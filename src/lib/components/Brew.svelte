<script lang="ts">
	import ProductCard, { type Product } from './ProductCard.svelte';

	const products: Product[] = [
		{
			id: 'classic-duriano',
			name: 'Classic Duriano',
			description: 'Medium roast, creamy finish.',
			price: '₱450',
			roast: 'Medium Roast',
			bestBrew: 'Pour-over (V60 or Chemex) at 92°C to reveal delicate floral durian aromatics and creamy citrus undertones.',
			servingTip: 'Sip black first to appreciate the balance, then add a splash of condensed milk for a silky Davao treat.',
			accentColor: 'var(--blue)',
			tintBg: 'var(--blue-tint)'
		},
		{
			id: 'dark-husk',
			name: 'Dark Husk',
			description: 'Dark roast, bold and smoky.',
			price: '₱480',
			roast: 'Dark Roast',
			bestBrew: 'French Press or traditional Moka Pot with coarse grind. 4 minutes steep for deep, smoky extraction.',
			servingTip: 'Stands up boldly to heavy cream or enjoyed alongside Davao tablea dark chocolate.',
			accentColor: 'var(--red)',
			tintBg: 'var(--red-tint)'
		},
		{
			id: 'iced-durian-latte-mix',
			name: 'Iced Durian Latte Mix',
			description: 'Ready-to-mix sachet.',
			price: '₱380',
			roast: 'Specialty Sachet (Box of 10)',
			bestBrew: 'Dissolve one sachet in 60ml warm water, stir vigorously until silky froth forms, then pour over ice.',
			servingTip: 'Top with chilled oat milk or fresh coconut milk for an instant tropical afternoon escape.',
			accentColor: 'var(--green)',
			tintBg: 'var(--green-tint)'
		}
	];
</script>

<section class="section brew-section" aria-labelledby="brew-title">
	<div class="container">
		<div class="brew-header">
			<div class="brand-dots" aria-hidden="true">
				<span class="brand-dot dot-blue"></span>
				<span class="brand-dot dot-yellow"></span>
				<span class="brand-dot dot-green"></span>
			</div>
			<h2 id="brew-title" class="brew-title">The Brew</h2>
			<p class="brew-intro">
				Crafted in limited small batches. Every roast harmonizes fresh highland beans with real Davao durian notes.
			</p>
		</div>

		<div class="products-grid">
			{#each products as product (product.id)}
				<ProductCard {product} />
			{/each}
		</div>
	</div>
</section>

<style>
	.brew-section {
		background-color: var(--white);
	}

	.brew-header {
		margin-bottom: 3rem;
		max-width: 44rem;
	}

	.brew-title {
		margin-bottom: 0.75rem;
	}

	.brew-intro {
		color: var(--grey);
		font-size: 1.125rem;
	}

	.products-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 1.5rem;
	}

	@media (min-width: 768px) {
		.products-grid {
			grid-template-columns: repeat(3, 1fr);
			gap: 2rem;
		}
	}
</style>
