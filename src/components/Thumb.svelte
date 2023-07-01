<script lang="ts">
	import { onDestroy, onMount } from 'svelte';

	export let side: 'L' | 'R';
	export let cx = 0,
		cy = 0,
		r = 42;

	let stickRef = {} as SVGCircleElement,
		holderRef = {} as SVGCircleElement,
		currentX = 0,
		currentY = 0,
		dx = 0,
		dy = 0;
	$: enableThumbMove = false;
	$: thumbX = 0;
	$: thumbY = 0;
	$: console.log(enableThumbMove);

	// onMount(() => {
	// 	if (typeof document == 'undefined') return;

	// 	document.addEventListener('mouseup', handleMouseup);
	// 	document.addEventListener('touchstart', handleTouchStart);
	// });

	// onDestroy(() => {
	// 	if (typeof document == 'undefined') return;
	// 	document.removeEventListener('mouseup', handleMouseup);
	// 	document.removeEventListener('touchstart', handleTouchStart);
	// });

	function handleMousedown(e: MouseEvent) {
		enableThumbMove = true;
		(currentX = e.clientX), (currentY = e.clientY);
	}

	// function handleMouseup(e: MouseEvent) {
	// 	enableThumbMove = false;
	// 	(thumbX = 0), (thumbY = 0);
	// }

	function handleMouseMove(e: MouseEvent) {
		if (!enableThumbMove || !stickRef.nodeName) return;
		const rect = stickRef.getBoundingClientRect();

		dx = ((e.clientX - currentX) * 100) / rect.width;
		dy = ((e.clientY - currentY) * 100) / rect.height;

		const _dx = (dx * 8) / 100;
		const _dy = (dy * 8) / 100;

		thumbX = _dx > 8 ? 8 : Math.round(_dx) < -8 ? -8 : Math.round(_dx);
		thumbY = _dy > 8 ? 8 : Math.round(_dy) < -8 ? -8 : Math.round(_dy);
		console.log(thumbX, thumbY);
	}

	function handleTouchEnd(e: TouchEvent) {
		enableThumbMove = false;
		(thumbX = 0), (thumbY = 0);
	}

	// function handleTouchStart(e: TouchEvent) {
	// 	enableThumbMove = true;
	// 	(currentX = e.touches[0].clientX), (currentY = e.touches[0].clientY);
	// }

	function handleTouchMove(e: TouchEvent) {
		if (!enableThumbMove || !stickRef.nodeName) return;
		const rect = stickRef.getBoundingClientRect();

		dx = ((e.touches[0].clientX - currentX) * 100) / rect.width;
		dy = ((e.touches[0].clientY - currentY) * 100) / rect.height;

		const _dx = (dx * 8) / 100;
		const _dy = (dy * 8) / 100;

		thumbX = _dx > 8 ? 8 : Math.round(_dx) < -8 ? -8 : Math.round(_dx);
		thumbY = _dy > 8 ? 8 : Math.round(_dy) < -8 ? -8 : Math.round(_dy);
	}
</script>

<!-- svelte-ignore a11y-interactive-supports-focus -->
<g data-role="thumb" data-name={`${side}Thumb`} aria-pressed="false">
	<circle id={`${side}holder`} class="cls-10" {cx} {cy} r={r + 30} />
	<!-- svelte-ignore a11y-interactive-supports-focus -->
	<circle
		id={`${side}stick`}
		class="cls-11 gamepad-btn"
		{cx}
		{cy}
		{r}
		data-role="thumb" data-name={`${side}Thumb`}
		role="button"
		aria-pressed="false"
	/>
</g>
