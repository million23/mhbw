<script>
	import { fade } from 'svelte/transition';

	export let image;
	let isFullscreen = false;

	console.log(image);
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<div on:click={() => (isFullscreen = true)} class="w-full h-full">
	<img src={image.src} alt={image.alt} class="w-full h-full cursor-pointer" />
</div>

{#if isFullscreen}
	<!-- svelte-ignore a11y-click-events-have-key-events -->
	<div
		transition:fade
		on:click={() => (isFullscreen = false)}
		class="fixed top-0 left-0 w-screen h-screen bg-black bg-opacity-50 z-[99] flex flex-col justify-center items-center"
	>
		<img src={image.src} alt={image.alt} class="w-[90%] h-[90%] object-cover" />
	</div>
{/if}
