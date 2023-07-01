<script lang="ts">
	import { onDestroy, onMount } from "svelte";
    import "../app.css";
    onMount(() => {
        if (typeof window == 'undefined') return;

        window.addEventListener('resize', changeOrientation);
    })

    onDestroy(() => {
        if (typeof window == 'undefined') return;

        window.removeEventListener('resize', changeOrientation);
    })
    
    async function changeOrientation () {
        if (typeof window == 'undefined') return;
        try {
            if (window.innerHeight < window.innerWidth) await screen.orientation.lock('landscape');
            else await screen.orientation.lock('portrait');
        } catch (error:any) {
            console.log("[Error]: ", error.message);
            window.removeEventListener('resize', changeOrientation);
        }
    }
  </script>
  
  <slot />