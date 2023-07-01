<script lang="ts">
	import { onDestroy, onMount } from 'svelte';
	import Thumb from './Thumb.svelte';

	let className = '';
	export { className as class };
	let currentX:number[] = [],
		currentY:number[] = [],
		dx = 0,
		dy = 0;

	onMount(() => {
		if (typeof window == 'undefined') return;
		window.addEventListener('touchstart', handleTouchStart);
		window.addEventListener('touchmove', handleTouchMove);
		window.addEventListener('touchend', handleTouchEnd);
	});

	onDestroy(() => {
		if (typeof window == 'undefined') return;
		// window.removeEventListener('mousedown', handleMouseDown);
		window.removeEventListener('touchstart', handleTouchStart);
		window.removeEventListener('touchmove', handleTouchMove);
		window.removeEventListener('touchend', handleTouchEnd);
	});

	function handleTouchStart(e: TouchEvent) {
		for (let i = 0; i < e.touches.length; i++) {
			const touch = e.touches[i];

			if ((touch.target as HTMLElement).dataset.role != 'thumb')
				console.log((touch.target as HTMLElement).dataset.name);
			else {
				currentX[i] = touch.clientX, currentY[i] = touch.clientY;
			}
		}
	}
	
	function handleTouchMove(e: TouchEvent) {
		for (let i = 0; i < e.touches.length; i++) {
			const touch = e.touches[i];
			
			const el = (touch.target as HTMLElement);
			
			if (el.dataset.role != 'thumb') return;
			const rect = el.getBoundingClientRect();
			dx = ((touch.clientX - currentX[i]) * 100) / rect.width;
			dy = ((touch.clientY - currentY[i]) * 100) / rect.height;
			
			dx = Math.min(dx, 100);
			dx = Math.max(dx, -100);

			dy = Math.min(dy, 100);
			dy = Math.max(dy, -100);
			const _dx = (dx * 8) / 100;
			const _dy = (dy * 8) / 100;
			
			const x = Math.round(_dx);
			const y = Math.round(_dy);

			el.style.transform = `translate(${x}%, ${y}%)`;
			console.log(el.dataset.name, x, y);
		}
	}

	function handleTouchEnd(e: TouchEvent) {
		const el = (e.target as HTMLElement);
		if (el.dataset.role !== 'thumb') return;
		el.style.transform = `translate(0%, 0%)`;
	}

	function handleMouseDown(e:MouseEvent) {
		console.log((e.target as HTMLElement).dataset.name)
	}
</script>

<svg
	id="Layer_1"
	class={className}
	data-name="Layer 1"
	xmlns="http://www.w3.org/2000/svg"
	xmlns:xlink="http://www.w3.org/1999/xlink"
	viewBox="0 0 843 525"
	><defs
		><style>
			.cls-1 {
				fill: #fff;
			}
			.cls-1,
			.cls-6 {
				fill-rule: evenodd;
			}
			.cls-2 {
				fill: #515151;
			}
			.cls-11,
			.cls-3,
			.cls-6 {
				fill: #f5f5f5;
			}
			.cls-11,
			.cls-3,
			.cls-6,
			.cls-8,
			.cls-9 {
				fill-opacity: 0.25;
			}
			.cls-10,
			.cls-4,
			.cls-5 {
				fill: none;
			}
			.cls-4,
			.cls-5 {
				stroke: #111;
				stroke-opacity: 0.9;
			}
			.cls-10,
			.cls-11,
			.cls-4,
			.cls-8 {
				stroke-width: 4px;
			}
			.cls-5 {
				stroke-width: 1.88px;
			}
			.cls-7 {
				mask: url(#mask);
			}
			.cls-8 {
				stroke: #000;
			}
			.cls-10,
			.cls-11 {
				stroke: #121212;
			}
		</style><mask
			id="mask"
			x="185.82"
			y="347.01"
			width="158"
			height="158"
			maskUnits="userSpaceOnUse"
			><g transform="translate(120 45)"
				><g id="path-16-inside-1_22_530" data-name="path-16-inside-1 22 530"
					><path
						class="cls-1"
						d="M111.82,406a8,8,0,0,1,8,8v34a8,8,0,0,0,8,8h34a8,8,0,0,0,8-8V414a8,8,0,0,1,8-8h34a8,8,0,0,0,8-8V364a8,8,0,0,0-8-8h-34a8,8,0,0,1-8-8V314a8,8,0,0,0-8-8h-34a8,8,0,0,0-8,8v34a8,8,0,0,1-8,8h-34a8,8,0,0,0-8,8v34a8,8,0,0,0,8,8Z"
					/></g
				></g
			></mask
		></defs
	>
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<g id="GAMEPAD"
		><rect id="BACKGROUND" class="cls-2" width="843" height="525" />
		<g
			id="START"
			class="gamepad-btn"
			tabindex="0"
			role="button"
			data-name="START"
			aria-pressed="false"
		>
			<circle data-name="START" class="cls-3" cx="318" cy="270" r="22" />
			<circle class="cls-4" cx="318" cy="270" r="20" data-name="START" />
		</g>
		<circle id="NOT_BUTTON" class="cls-4" cx="385.82" cy="170.66" r="33.7" />
		<g
			id="RESET"
			tabindex="0"
			class="gamepad-btn"
			role="button"
			data-name="RESET"
			aria-pressed="false"
			><circle data-name="RESET" class="cls-3" cx="453" cy="270" r="22" /><circle
				class="cls-4"
				cx="453"
				cy="270"
				r="20"
				data-name="RESET"
			/><rect
				class="cls-5"
				x="445.09"
				y="262.09"
				width="16.91"
				height="1.88"
				rx="0.94"
				data-name="RESET"
			/><rect
				class="cls-5"
				x="445.09"
				y="269.61"
				width="16.91"
				height="1.88"
				rx="0.94"
				data-name="RESET"
			/><rect
				data-name="RESET"
				class="cls-5"
				x="445.09"
				y="277.12"
				width="16.91"
				height="1.88"
				rx="0.94"
			/></g
		><g id="Arrows" style="transform: translate(-20px, -45px) scale(1.085);">
			<path
				class="cls-6"
				d="M111.82,406a8,8,0,0,1,8,8v34a8,8,0,0,0,8,8h34a8,8,0,0,0,8-8V414a8,8,0,0,1,8-8h34a8,8,0,0,0,8-8V364a8,8,0,0,0-8-8h-34a8,8,0,0,1-8-8V314a8,8,0,0,0-8-8h-34a8,8,0,0,0-8,8v34a8,8,0,0,1-8,8h-34a8,8,0,0,0-8,8v34a8,8,0,0,0,8,8Z"
				transform="translate(120 45)"
			/>
			<g class="cls-7"
				><path
					id="LRUD"
					d="M77.82,356v0Zm34,0v0Zm16-50v0Zm42,8h0Zm-8-8v0Zm16,50v0Zm34,0v0Zm-42,58h0Zm8-8v0Zm-66,0v0Zm12,42V414h-8v34Zm38,4h-34v8h34Zm4-38v34h8V414Zm46-12h-34v8h34Zm4-38v34h8V364Zm-38-4h34v-8h-34Zm-12-46v34h8V314Zm-38-4h34v-8h-34Zm-4,38V314h-8v34Zm-46,12h34v-8h-34Zm-4,38V364h-8v34Zm38,4h-34v8h34Zm-46-4a12,12,0,0,0,12,12v-8a4,4,0,0,1-4-4Zm12-46a12,12,0,0,0-12,12h8a4,4,0,0,1,4-4Zm38-4a4,4,0,0,1-4,4v8a12,12,0,0,0,12-12Zm12-46a12,12,0,0,0-12,12h8a4,4,0,0,1,4-4Zm46,12a12,12,0,0,0-12-12v8a4,4,0,0,1,4,4Zm4,38a4,4,0,0,1-4-4h-8a12,12,0,0,0,12,12Zm46,12a12,12,0,0,0-12-12v8a4,4,0,0,1,4,4Zm-12,46a12,12,0,0,0,12-12h-8a4,4,0,0,1-4,4Zm-38,4a4,4,0,0,1,4-4v-8a12,12,0,0,0-12,12Zm-12,46a12,12,0,0,0,12-12h-8a4,4,0,0,1-4,4Zm-38-46a12,12,0,0,0-12-12v8a4,4,0,0,1,4,4Zm-8,34a12,12,0,0,0,12,12v-8a4,4,0,0,1-4-4Z"
					transform="translate(120 45)"
				/></g
			><circle id="Center" class="cls-8" cx="264.82" cy="426.01" r="15" />
			<rect
				id="DOWN"
				data-name="DOWN"
				class="cls-9 gamepad-btn"
				tabindex="0"
				role="button"
				aria-pressed="false"
				x="241"
				y="454"
				width="47"
				height="45"
			/>
			<rect
				id="UP"
				data-name="UP"
				class="cls-9 gamepad-btn"
				tabindex="0"
				role="button"
				aria-pressed="false"
				x="241"
				y="354"
				width="47"
				height="45"
			/>
			<rect
				id="RIGHT"
				data-name="RIGHT"
				class="cls-9 gamepad-btn"
				tabindex="0"
				role="button"
				aria-pressed="false"
				x="170.25"
				y="357.25"
				width="47"
				height="47.5"
				transform="translate(-67.25 619.75) rotate(-90)"
			/><rect
				id="LEFT"
				data-name="LEFT"
				class="cls-9 gamepad-btn"
				tabindex="0"
				role="button"
				aria-pressed="false"
				x="72"
				y="358"
				width="47"
				height="47"
				transform="translate(-166 522) rotate(-90)"
			/></g
		>
		<Thumb side="R" cx={512} cy={416} r={32}/>
        <Thumb side="L" cx={145} cy={275} r={32}/>
		<g id="Y" data-name="Y" class="gamepad-btn" tabindex="0" role="button" aria-pressed="false"
			><circle data-name="Y" class="cls-3" cx="628" cy="210" r="30" />
			<circle data-name="Y" class="cls-4" cx="628" cy="210" r="28" />
			<path
				data-name="Y"
				d="M516.28,154.71c1,.7,1.52,1.39,1.52,2a3.38,3.38,0,0,1-.71,1.64l-6.7,10v5.92a7.38,7.38,0,0,1-.06,1.09,2.11,2.11,0,0,1-.28.81,1.35,1.35,0,0,1-.84.65,7,7,0,0,1-3.16,0,1.36,1.36,0,0,1-.83-.65,3.28,3.28,0,0,1-.31-.84,10.47,10.47,0,0,1,0-1.12v-5.86l-6.69-10a3.29,3.29,0,0,1-.71-1.64,2.42,2.42,0,0,1,1.36-1.89,4.4,4.4,0,0,1,1.95-.93,1.6,1.6,0,0,1,.93.24,4.29,4.29,0,0,1,1.12,1.27l4.8,7.69,4.81-7.69a3.86,3.86,0,0,1,1-1.2,1.64,1.64,0,0,1,1-.31A4,4,0,0,1,516.28,154.71Z"
				transform="translate(120 45)"
			/>
		</g>
		<g id="A" data-name="A" class="gamepad-btn" tabindex="0" role="button" aria-pressed="false"
			><circle data-name="A" class="cls-3" cx="628" cy="335" r="30" />
			<circle data-name="A" class="cls-4" cx="628" cy="335" r="28" />
			<path
				data-name="A"
				d="M510.35,280.89l8.37,17.3a4.08,4.08,0,0,1,.53,1.58q0,1.11-1.8,2a4.1,4.1,0,0,1-1.67.53,1.65,1.65,0,0,1-1-.28,2.05,2.05,0,0,1-.56-.59c-.1-.21-.26-.52-.47-.93l-1.61-3.35h-8.59L502,300.51c-.21.41-.37.71-.49.9a2.15,2.15,0,0,1-.56.59,1.59,1.59,0,0,1-1,.28,4.12,4.12,0,0,1-1.65-.53c-1.2-.58-1.79-1.24-1.79-2a4,4,0,0,1,.52-1.58l8.37-17.33a2.72,2.72,0,0,1,1-1.15,2.79,2.79,0,0,1,1.48-.43A2.6,2.6,0,0,1,510.35,280.89Zm-2.51,7.44-2,4.25h4.12Z"
				transform="translate(120 45)"
			/>
		</g>
		<g id="X" data-name="X" class="gamepad-btn" tabindex="0" role="button" aria-pressed="false"
			><circle data-name="X" class="cls-3" cx="566" cy="272" r="30" /><circle
				class="cls-4"
				data-name="X"
				cx="566"
				cy="272"
				r="28"
			/><path
				data-name="X"
				d="M450.22,227.5l6.23,6.85a3.32,3.32,0,0,1,1.06,2,2.92,2.92,0,0,1-1.21,1.89,3.29,3.29,0,0,1-2,1.09c-.54,0-1.17-.41-1.89-1.24l-5.89-6.76-5.89,6.76a3,3,0,0,1-1.92,1.24,3.5,3.5,0,0,1-2-1.09,3,3,0,0,1-1.2-1.89,3.43,3.43,0,0,1,1.08-2l6.23-6.85-6.23-6.85a3.21,3.21,0,0,1-1.08-2,2.93,2.93,0,0,1,1.2-1.9,3.39,3.39,0,0,1,2-1.11,2.87,2.87,0,0,1,1.92,1.24l5.89,6.76,5.89-6.76c.75-.83,1.38-1.24,1.89-1.24a3.42,3.42,0,0,1,2,1.08,3,3,0,0,1,1.21,1.93,3.12,3.12,0,0,1-1.06,2Z"
				transform="translate(120 45)"
			/></g
		><g id="B" data-name="B" class="gamepad-btn" tabindex="0" role="button" aria-pressed="false"
			><circle data-name="B" class="cls-3" cx="692" cy="272" r="30" /><circle
				class="cls-4"
				data-name="B"
				cx="692"
				cy="272"
				r="28"
			/><path
				data-name="B"
				d="M579.42,226.82a7.39,7.39,0,0,1-.31,10.07,6.72,6.72,0,0,1-5,2.08H566c-1.45,0-2.3-.39-2.54-1.18a5,5,0,0,1-.19-1.61V219q0-.74,0-1.08a3,3,0,0,1,.31-.81c.29-.55,1.1-.83,2.42-.83h7.81a6.41,6.41,0,0,1,4.78,2,6.59,6.59,0,0,1,2,4.84A6.44,6.44,0,0,1,579.42,226.82Zm-3.66,4.55a3.09,3.09,0,0,0-.18-1.17,1,1,0,0,0-.56-.62,4.71,4.71,0,0,0-1.74-.25,2.69,2.69,0,0,1-1.67-.44,2.16,2.16,0,0,1-.56-1.76,2.23,2.23,0,0,1,.56-1.8,3.28,3.28,0,0,1,1.92-.43c.83,0,1.32-.22,1.49-.66a4.74,4.74,0,0,0,.09-1.11,1.16,1.16,0,0,0-.52-1.09,3,3,0,0,0-1.52-.31h-4.34v11.75h5.08C575.11,233.48,575.76,232.78,575.76,231.37Z"
				transform="translate(120 45)"
			/></g
		>
		<g id="LB" data-name="LB" class="gamepad-btn" tabindex="0" role="button" aria-pressed="false"
			><path
				data-name="LB"
				class="cls-3"
				d="M-68.89,13.14A46.5,46.5,0,0,1-51.73,5l50-12.11L60.72-16l64.21-2.56a18.7,18.7,0,0,1,16.37,8.43l20.38,31.07a9.34,9.34,0,0,1-8.44,14.45L86.33,30.84a18.74,18.74,0,0,0-13.94,4.9l-11,10.1a18.69,18.69,0,0,1-13.21,4.94L-7,49.2a18.67,18.67,0,0,1-6.87-1.53L-67.5,24.56a6.66,6.66,0,0,1-1.39-11.42Z"
				transform="translate(120 45)"
			/><path
				data-name="LB"
				class="cls-4"
				d="M-1.33-5.13,60.9-14,125-16.58a16.71,16.71,0,0,1,14.62,7.52L160,22a7.35,7.35,0,0,1-6.64,11.36L86.46,28.84A20.71,20.71,0,0,0,71,34.27l-11,10.1a16.67,16.67,0,0,1-11.79,4.41L-7,47.2a16.81,16.81,0,0,1-6.13-1.36l-53.6-23.11a4.66,4.66,0,0,1-1-8A44.5,44.5,0,0,1-51.26,7Z"
				transform="translate(120 45)"
			/><path
				data-name="LB"
				d="M20.49,37.14h8.43a3.39,3.39,0,0,1,1.49.25,1.12,1.12,0,0,1,.62.71,4.41,4.41,0,0,1,.16,1.34,4.26,4.26,0,0,1-.16,1.3,1.06,1.06,0,0,1-.52.68,3.48,3.48,0,0,1-1.62.31H17.73c-1.44,0-2.29-.39-2.54-1.18A5,5,0,0,1,15,39V21.74c0-.48,0-.83,0-1.06a2.64,2.64,0,0,1,.31-.84c.29-.55,1.09-.83,2.42-.83s2.3.38,2.57,1.14a6.45,6.45,0,0,1,.15,1.62Zm28.89-7.59a7.39,7.39,0,0,1-.31,10.07,6.7,6.7,0,0,1-5,2.08H35.93c-1.45,0-2.29-.39-2.54-1.18a5,5,0,0,1-.19-1.61V21.7q0-.73,0-1.08a3,3,0,0,1,.31-.81c.29-.55,1.1-.83,2.42-.83h7.81a6.41,6.41,0,0,1,4.78,2,6.59,6.59,0,0,1,2,4.84A6.44,6.44,0,0,1,49.38,29.55ZM45.73,34.1a3.06,3.06,0,0,0-.19-1.17,1,1,0,0,0-.56-.62,4.71,4.71,0,0,0-1.74-.25,2.69,2.69,0,0,1-1.67-.44A2.15,2.15,0,0,1,41,29.86a2.23,2.23,0,0,1,.56-1.8,3.28,3.28,0,0,1,1.92-.43c.83,0,1.33-.22,1.49-.66a4.74,4.74,0,0,0,.09-1.11,1.16,1.16,0,0,0-.52-1.09A3,3,0,0,0,43,24.46H38.69V36.21h5.08C45.07,36.21,45.73,35.51,45.73,34.1Z"
				transform="translate(120 45)"
			/></g
		><g id="LT" data-name="LT" class="gamepad-btn" tabindex="0" role="button" aria-pressed="false"
			><path
				data-name="LT"
				class="cls-3"
				d="M-54.36,83A59.82,59.82,0,0,0-5.64,119.24l11.58,1.25A48,48,0,0,0,57.73,83.92h0A15,15,0,0,0,43.61,65.46L8.2,64.36A37.25,37.25,0,0,1-6.65,60.79L-60.29,35.38a7.48,7.48,0,0,0-10.09,9.67Z"
				transform="translate(120 45)"
			/><path
				data-name="LT"
				class="cls-4"
				d="M-5.42,117.26,6.16,118.5a46,46,0,0,0,49.63-35,13,13,0,0,0-12.24-16L8.14,66.36A39.3,39.3,0,0,1-7.51,62.59l-53.64-25.4a5.48,5.48,0,0,0-7.39,7.08l16,38A57.82,57.82,0,0,0-5.42,117.26Z"
				transform="translate(120 45)"
			/><path
				data-name="LT"
				d="M-1.12,98.54H7.31a3.39,3.39,0,0,1,1.49.25,1.1,1.1,0,0,1,.62.71,4.41,4.41,0,0,1,.16,1.34,4.26,4.26,0,0,1-.16,1.3,1,1,0,0,1-.53.68,3.44,3.44,0,0,1-1.61.31H-3.88c-1.44,0-2.29-.39-2.54-1.18a5,5,0,0,1-.19-1.58V83.14c0-.48,0-.83,0-1.06a2.64,2.64,0,0,1,.31-.84c.29-.55,1.09-.83,2.41-.83s2.31.38,2.58,1.14a6.39,6.39,0,0,1,.15,1.62Zm14.2-18.16H30.31a3.32,3.32,0,0,1,1.46.24,1.14,1.14,0,0,1,.62.72,5.36,5.36,0,0,1,0,2.6,1,1,0,0,1-.53.65,3.55,3.55,0,0,1-1.58.28H24.36v15.59a6.75,6.75,0,0,1-.06,1.06,2.13,2.13,0,0,1-.28.8,1.23,1.23,0,0,1-.81.62,5,5,0,0,1-1.54.19,5.14,5.14,0,0,1-1.56-.19,1.35,1.35,0,0,1-.8-.62,3.21,3.21,0,0,1-.28-.8c0-.25,0-.61,0-1.09V84.87H13.05a3.57,3.57,0,0,1-1.46-.22,1.2,1.2,0,0,1-.62-.74,4.64,4.64,0,0,1-.15-1.3A4.27,4.27,0,0,1,11,81.34a1.09,1.09,0,0,1,.53-.69A3.71,3.71,0,0,1,13.08,80.38Z"
				transform="translate(120 45)"
			/></g
		><g id="RT" data-name="RT" class="gamepad-btn" tabindex="0" role="button" aria-pressed="false"
			><path
				data-name="RT"
				class="cls-3"
				d="M653.36,83a59.82,59.82,0,0,1-48.72,36.22l-11.58,1.25a48,48,0,0,1-51.79-36.57h0a15,15,0,0,1,14.12-18.46l35.41-1.1a37.25,37.25,0,0,0,14.85-3.57l53.64-25.41a7.48,7.48,0,0,1,10.09,9.67Z"
				transform="translate(120 45)"
			/><path
				data-name="RT"
				class="cls-4"
				d="M604.42,117.26l-11.58,1.24a46,46,0,0,1-49.63-35,13,13,0,0,1,12.24-16l35.41-1.1a39.3,39.3,0,0,0,15.65-3.77l53.64-25.4a5.48,5.48,0,0,1,7.39,7.08l-16,38A57.82,57.82,0,0,1,604.42,117.26Z"
				transform="translate(120 45)"
			/><path
				data-name="RT"
				d="M585.08,99.29a4.93,4.93,0,0,1,.47,1.61c0,.78-.64,1.45-1.93,2a4.25,4.25,0,0,1-1.61.44,1.75,1.75,0,0,1-1-.28,2.82,2.82,0,0,1-.56-.62q-.3-.6-2.42-5.61l-1,.06h-3.9v3.5a6,6,0,0,1-.07,1.09,2.28,2.28,0,0,1-.27.8c-.29.56-1.1.84-2.42.84s-2.3-.38-2.54-1.15a5,5,0,0,1-.19-1.61V83.14c0-.48,0-.83,0-1.06a2.91,2.91,0,0,1,.31-.84c.29-.55,1.1-.83,2.42-.83h6.7a8.63,8.63,0,0,1,5.3,2,7.28,7.28,0,0,1,2,2.6,8.19,8.19,0,0,1,.81,3.66A7.71,7.71,0,0,1,583,94.42C583.43,95.51,584.13,97.14,585.08,99.29Zm-11.9-7.91h4a3,3,0,0,0,1.79-.68,2.42,2.42,0,0,0,.9-2,2.39,2.39,0,0,0-.9-2,3,3,0,0,0-1.86-.72h-3.9Zm14.31-11h17.24a3.35,3.35,0,0,1,1.46.24,1.17,1.17,0,0,1,.62.72,5.71,5.71,0,0,1,0,2.6,1.07,1.07,0,0,1-.53.65,3.55,3.55,0,0,1-1.58.28h-5.92v15.59a6.75,6.75,0,0,1-.06,1.06,2.33,2.33,0,0,1-.28.8,1.28,1.28,0,0,1-.81.62,6.42,6.42,0,0,1-3.1,0,1.4,1.4,0,0,1-.81-.62,3.58,3.58,0,0,1-.27-.8,10.08,10.08,0,0,1,0-1.09V84.87h-5.95a3.51,3.51,0,0,1-1.45-.22,1.2,1.2,0,0,1-.62-.74,4.26,4.26,0,0,1-.16-1.3,3.93,3.93,0,0,1,.16-1.27,1.08,1.08,0,0,1,.52-.69A3.71,3.71,0,0,1,587.49,80.38Z"
				transform="translate(120 45)"
			/></g
		><g id="RB" class="gamepad-btn" tabindex="0" data-name="RB" role="button" aria-pressed="false"
			><path
				class="cls-3"
				d="M667.88,13.14A46.45,46.45,0,0,0,650.73,5l-50-12.11L538.28-16l-64.21-2.56a18.7,18.7,0,0,0-16.37,8.43L437.32,20.92a9.34,9.34,0,0,0,8.44,14.45l66.91-4.53a18.7,18.7,0,0,1,13.93,4.9l11,10.1a18.69,18.69,0,0,0,13.21,4.94L606,49.2a18.67,18.67,0,0,0,6.87-1.53l53.6-23.11a6.65,6.65,0,0,0,1.38-11.42Z"
				transform="translate(120 45)"
				data-name="RB"
			/><path
				data-name="RB"
				class="cls-4"
				d="M600.33-5.13,538.1-14,474-16.58a16.71,16.71,0,0,0-14.62,7.52L439,22a7.35,7.35,0,0,0,6.64,11.36l66.91-4.53A20.71,20.71,0,0,1,528,34.27l10.95,10.1a16.71,16.71,0,0,0,11.8,4.41L606,47.2a16.82,16.82,0,0,0,6.14-1.36l53.6-23.11a4.66,4.66,0,0,0,1-8A44.5,44.5,0,0,0,650.26,7Z"
				transform="translate(120 45)"
			/><path
				data-name="RB"
				d="M570.29,33.92a4.93,4.93,0,0,1,.47,1.61q0,1.19-1.92,2a4.34,4.34,0,0,1-1.62.44,1.75,1.75,0,0,1-1-.28,2.62,2.62,0,0,1-.56-.62c-.2-.39-1-2.26-2.41-5.61l-1,.06h-3.9V35a7.38,7.38,0,0,1-.06,1.09,2.26,2.26,0,0,1-.28.8c-.29.56-1.1.84-2.42.84s-2.29-.38-2.54-1.15A4.94,4.94,0,0,1,552.9,35V17.77c0-.48,0-.83,0-1.06a2.86,2.86,0,0,1,.31-.83c.29-.56,1.1-.84,2.42-.84h6.7a8.63,8.63,0,0,1,5.3,2,7.23,7.23,0,0,1,2,2.61,8.13,8.13,0,0,1,.81,3.66,7.7,7.7,0,0,1-2.33,5.76Q568.87,30.7,570.29,33.92ZM558.39,26h4a2.91,2.91,0,0,0,1.79-.68,2.4,2.4,0,0,0,.9-2,2.41,2.41,0,0,0-.9-2.05,2.94,2.94,0,0,0-1.86-.71h-3.9Zm30.25-.43a7.39,7.39,0,0,1-.31,10.07,6.72,6.72,0,0,1-5,2.08h-8.15c-1.45,0-2.3-.39-2.55-1.18a5.34,5.34,0,0,1-.18-1.61V17.74c0-.5,0-.86,0-1.09a2.55,2.55,0,0,1,.31-.8c.29-.56,1.09-.84,2.42-.84H583a6.38,6.38,0,0,1,4.77,2,6.6,6.6,0,0,1,2,4.84A6.51,6.51,0,0,1,588.64,25.58ZM585,30.14A3.14,3.14,0,0,0,584.8,29a1,1,0,0,0-.56-.62,4.71,4.71,0,0,0-1.74-.25,2.69,2.69,0,0,1-1.67-.43,2.18,2.18,0,0,1-.56-1.77,2.23,2.23,0,0,1,.56-1.8,3.28,3.28,0,0,1,1.92-.43c.83,0,1.32-.22,1.49-.65a4.9,4.9,0,0,0,.09-1.12,1.15,1.15,0,0,0-.53-1.09,3,3,0,0,0-1.52-.31H578V32.24H583Q585,32.24,585,30.14Z"
				transform="translate(120 45)"
			/></g
		></g
	></svg
>
