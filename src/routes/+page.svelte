<script lang="ts">
	import Hero from '../lib/components/Hero.svelte';
	import Story from '../lib/components/Story.svelte';
	import Brew from '../lib/components/Brew.svelte';
	import HowToEnjoy from '../lib/components/HowToEnjoy.svelte';
	import Reviews from '../lib/components/Reviews.svelte';
	import FinalCta from '../lib/components/FinalCta.svelte';
	import DevFest from '../lib/components/DevFest.svelte';
	import Footer from '../lib/components/Footer.svelte';
</script>

<svelte:head>
	<title>Duriano Coffee — Bold like Davao. Smells like a story.</title>
	<meta
		name="description"
		content="Small-batch coffee infused with Davao durian. Creamy, bold, unapologetic. Experience the signature roast from Davao City."
	/>
	<meta property="og:title" content="Duriano Coffee — Bold like Davao. Smells like a story." />
	<meta
		property="og:description"
		content="Small-batch coffee infused with Davao durian. Creamy, bold, unapologetic."
	/>
	<meta property="og:image" content="/favicon.svg" />
	<meta property="og:type" content="website" />
</svelte:head>

<main id="main-content">
	<!-- 1. Hero -->
	<Hero />

	<!-- 2. Story -->
	<Story />

	<!-- 3. The Brew -->
	<Brew />

	<!-- 4. How to enjoy it -->
	<HowToEnjoy />

	<!-- 5. Sample reviews -->
	<Reviews />

	<!-- 6. Final CTA -->
	<FinalCta />

	<!-- 7. DevFest Davao 2026 (Easter Egg) -->
	<DevFest />
</main>

<!-- 8. Footer -->
<Footer />

<style>
	main {
		display: flex;
		flex-direction: column;
		width: 100%;
	}
</style>
