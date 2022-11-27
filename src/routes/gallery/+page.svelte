<script>
	import { onMount } from 'svelte';
	import ReactiveImage from '../../components/Image.svelte';
	import client from '../../lib/urqlClient';

	let images = [];

	let query = `
		{
			galleryItems {
				id
				mainImage {
					url
				}
				imageCaption
			}
		}
	`;

	onMount(async () => {
		const { galleryItems } = await client.request(query);

		console.table(galleryItems);

		images = galleryItems?.map((item) => ({
			id: item.id,
			src: item.mainImage.url,
			alt: item.imageCaption
		}));
	});

	// 10 random images from lorem picsum
	// const images = Array.from({ length: 10 }, (_, i) => ({
	// 	src: `https://picsum.photos/400/300?random=${i}`,
	// 	alt: `Image ${i}`
	// }));
</script>

<svelte:head>
	<title>Gallery | Mental Health is the Best Wealth</title>
</svelte:head>

<main class="relative w-full flex justify-center pt-48 pb-10 px-5 lg:px-0">
	<img
		src="https://images.unsplash.com/photo-1579547621706-1a9c79d5c9f1?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80"
		alt="background"
		class="absolute object-cover object-top w-full h-full top-0 left-0 -z-30"
	/>
	<section class="w-full max-w-4xl">
		<h1 class="text-4xl font-bold">Our Gallery</h1>
		<p class="text-xl font-semibold max-w-md">
			See what we have been up to and what we have achieved. Take a look at our gallery. You can
			also share your photos with us via email.
		</p>
		<span class="material-symbols-outlined text-3xl mt-10 animate-bounce">expand_more</span>
	</section>
</main>

<main class="relative w-full flex justify-center py-10 px-5 lg:px-0">
	<section class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-2 w-full max-w-4xl relative">
		{#each images as image}
			<ReactiveImage {image} />
		{/each}
	</section>
</main>
