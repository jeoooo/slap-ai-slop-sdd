<script lang="ts">
	interface Review {
		id: string;
		author: string;
		role: string;
		quote: string;
		tint: string;
	}

	const reviews: Review[] = [
		{
			id: 'rev-1',
			author: 'Bea R.',
			role: 'Home Brewer, Matina',
			quote:
				'I honestly bought this for the sheer novelty, but Classic Duriano became my everyday morning brew. The custard aftertaste is unbelievable.',
			tint: 'var(--blue-tint)'
		},
		{
			id: 'rev-2',
			author: 'Carlos M.',
			role: 'Coffee Enthusiast, Bajada',
			quote:
				'Dark Husk delivers on every promise. It is rich, smoky, and completely owns the Davao durian aroma. It converted every doubter in my office.',
			tint: 'var(--yellow-tint)'
		},
		{
			id: 'rev-3',
			author: 'Lianne T.',
			role: 'Graphic Artist, Lanang',
			quote:
				'The Iced Durian Latte Mix is a game changer for mid-afternoon slumps. Silky sweet, fragrant, and shockingly smooth over ice.',
			tint: 'var(--green-tint)'
		}
	];
</script>

<section class="section reviews-section" aria-labelledby="reviews-title">
	<div class="container">
		<div class="reviews-header">
			<div class="demo-badge">
				<span>Sample reviews for demo.</span>
			</div>

			<h2 id="reviews-title" class="reviews-title">What brave tasters are saying</h2>
			<p class="reviews-intro">
				Real reactions to our small-batch blends. Unfiltered curiosity turned into morning ritual.
			</p>
		</div>

		<div class="reviews-grid">
			{#each reviews as review (review.id)}
				<figure class="review-card" style="background-color: {review.tint};">
					<blockquote class="review-quote">
						<p>“{review.quote}”</p>
					</blockquote>
					<figcaption class="review-author">
						<span class="author-name">{review.author}</span>
						<span class="author-role">{review.role}</span>
					</figcaption>
				</figure>
			{/each}
		</div>
	</div>
</section>

<style>
	.reviews-section {
		background-color: var(--white);
	}

	.reviews-header {
		margin-bottom: 3rem;
		max-width: 44rem;
	}

	.demo-badge {
		display: inline-block;
		background-color: var(--surface);
		color: var(--grey);
		font-size: 0.8125rem;
		font-weight: 600;
		padding: 0.25rem 0.75rem;
		border-radius: var(--radius-pill);
		border: 1px solid rgba(32, 33, 36, 0.12);
		margin-bottom: 1.25rem;
		text-transform: uppercase;
		letter-spacing: 0.04em;
	}

	.reviews-title {
		margin-bottom: 0.75rem;
	}

	.reviews-intro {
		color: var(--grey);
		font-size: 1.125rem;
	}

	.reviews-grid {
		display: grid;
		grid-template-columns: 1fr;
		gap: 1.5rem;
	}

	@media (min-width: 768px) {
		.reviews-grid {
			grid-template-columns: repeat(3, 1fr);
			gap: 2rem;
		}
	}

	.review-card {
		padding: 2rem;
		border-radius: var(--radius-card);
		border: 1px solid rgba(32, 33, 36, 0.08);
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		height: 100%;
	}

	.review-quote {
		margin-bottom: 1.5rem;
	}

	.review-quote p {
		color: var(--ink);
		font-size: 1.05rem;
		line-height: 1.6;
		font-style: italic;
	}

	.review-author {
		display: flex;
		flex-direction: column;
		gap: 0.125rem;
		border-top: 1px solid rgba(32, 33, 36, 0.1);
		padding-top: 1rem;
	}

	.author-name {
		font-weight: 700;
		color: var(--ink);
		font-size: 1rem;
	}

	.author-role {
		font-size: 0.875rem;
		color: var(--grey);
	}
</style>
