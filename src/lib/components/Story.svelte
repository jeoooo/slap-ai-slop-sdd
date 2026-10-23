<script lang="ts">
</script>

<section class="section section-surface story-section" aria-labelledby="story-title">
	<div class="container story-grid">
		<div class="story-content">
			<div class="brand-dots" aria-hidden="true">
				<span class="brand-dot dot-yellow"></span>
				<span class="brand-dot dot-red"></span>
			</div>
			<h2 id="story-title" class="story-title">Born at the foot of Mount Apo</h2>

			<div class="story-paragraphs">
				<p>
					It started as an audacious kitchen dare in downtown Davao. What happens when you take the King of Fruits—famous for its velvety custard texture and notorious aroma—and roast it alongside heritage highland coffee beans? Most folks told us we were completely crazy. But one slow pour revealed an undeniably rich, buttery cup with sweet notes of tropical caramel and cacao.
				</p>
				<p>
					We slow-infuse ripened Davao Puyat durian into micro-lots of Arabica and Robusta, balancing pungent tropical aroma with a deeply chocolatey body. The initial scent is unmistakably bold, but the first sip is pure silky comfort. No shortcuts, no artificial extracts, just real fruit and fire.
				</p>
				<p>
					Whether you are a lifelong durian devotee or a curious skeptic who wrinkles their nose at the fruit stalls along Magsaysay Park, this brew welcomes you with open arms. <em>Sulayi na!</em> Take that first fearless sip and let the conversation begin.
				</p>
			</div>
		</div>

		<figure class="story-figure">
			<img
				src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcShaSOX18UCBMi7_x_5FiTctMhrrDVU47oUehiJKSZLQA77nFS2rW3XxnCh&s=10"
				alt="Golden sculpture of a family carved inside a giant split-open durian, under a bright Davao sky"
				width="556"
				height="552"
				loading="lazy"
			/>
		</figure>
	</div>
</section>

<style>
	.story-section {
		border-top: 1px solid rgba(32, 33, 36, 0.08);
		border-bottom: 1px solid rgba(32, 33, 36, 0.08);
	}

	.story-grid {
		display: grid;
		gap: 2rem;
		align-items: center;
	}

	.story-figure img {
		display: block;
		width: 100%;
		height: auto;
		border-radius: var(--radius-card);
		border: 1px solid rgba(32, 33, 36, 0.12);
	}

	@media (min-width: 768px) {
		.story-grid {
			grid-template-columns: 1.2fr 1fr;
			gap: 3rem;
		}
	}

	.story-content {
		max-width: 48rem;
	}

	.story-title {
		margin-bottom: 1.75rem;
	}

	.story-paragraphs {
		display: flex;
		flex-direction: column;
		gap: 1.25rem;
	}

	.story-paragraphs p {
		color: var(--ink);
		line-height: 1.7;
	}

	.story-paragraphs em {
		font-style: italic;
		font-weight: 500;
		color: var(--blue-text);
	}
</style>
