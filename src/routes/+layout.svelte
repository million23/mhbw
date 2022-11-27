<script>
	import '../app.css';
	import Footer from '../components/Footer.svelte';
	import Topbar from '../components/Topbar.svelte';
</script>

<svelte:head>
	<title>Mental Health is the Best Wealth</title>
</svelte:head>

<Topbar />
<main class="min-h-screen">
	<slot />
</main>
<Footer />
