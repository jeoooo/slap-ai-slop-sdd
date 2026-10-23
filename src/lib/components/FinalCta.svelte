<script lang="ts">
	interface Props {
		reserveEmail?: string;
	}

	let { reserveEmail = 'hello@durianocoffee.demo' }: Props = $props();
</script>

<section class="section section-dark final-cta-section" aria-labelledby="final-cta-title">
	<div class="container final-cta-container">
		<div class="brand-dots" aria-hidden="true">
			<span class="brand-dot dot-blue"></span>
			<span class="brand-dot dot-red"></span>
			<span class="brand-dot dot-yellow"></span>
			<span class="brand-dot dot-green"></span>
		</div>

		<h2 id="final-cta-title" class="final-cta-title">
			Ready to taste the boldest cup in Davao?
		</h2>

		<p class="final-cta-desc">
			Batches are roasted every Tuesday in limited quantities. Send us your reservation and we’ll reserve your fresh pack with zero commitment.
		</p>

		<div class="final-cta-action">
			<a
				href="mailto:{reserveEmail}?subject=Reserve%20a%20pack%20of%20Duriano%20Coffee"
				class="btn btn-primary final-cta-btn"
			>
				Reserve a pack
			</a>
		</div>

		<p class="final-cta-note">
			Freshly ground or whole bean · Delivered right to your doorstep in Davao City
		</p>
	</div>
</section>

<style>
	.final-cta-section {
		text-align: center;
		padding-top: 5rem;
		padding-bottom: 5rem;
	}

	.final-cta-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.final-cta-title {
		max-width: 22ch;
		margin-bottom: 1.25rem;
		color: var(--white);
	}

	.final-cta-desc {
		max-width: 46ch;
		font-size: 1.15rem;
		color: #BDC1C6;
		margin-bottom: 2.25rem;
	}

	.final-cta-action {
		margin-bottom: 1.25rem;
	}

	.final-cta-btn {
		font-size: 1.125rem;
	}

	.final-cta-note {
		font-size: 0.875rem;
		color: #9AA0A6;
	}
</style>
