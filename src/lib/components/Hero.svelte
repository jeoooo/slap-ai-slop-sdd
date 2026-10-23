<script lang="ts">
	interface Props {
		reserveEmail?: string;
	}

	let { reserveEmail = 'reserve@durianocoffee.demo' }: Props = $props();
</script>

<section class="section hero-section" aria-labelledby="hero-title">
	<div class="container hero-container">
		<div class="brand-dots" aria-hidden="true">
			<span class="brand-dot dot-blue"></span>
			<span class="brand-dot dot-red"></span>
			<span class="brand-dot dot-yellow"></span>
			<span class="brand-dot dot-green"></span>
		</div>

		<div class="brand-badge">
			<span>Duriano Coffee · Davao City</span>
		</div>

		<h1 id="hero-title" class="hero-title">
			Coffee that dares you to smell it first.
		</h1>

		<p class="hero-subtitle">
			Small-batch coffee infused with Davao durian. Creamy, bold, unapologetic.
		</p>

		<div class="hero-cta-wrapper">
			<a
				href="mailto:{reserveEmail}?subject=Reserve%20a%20pack%20of%20Duriano%20Coffee"
				class="btn btn-primary hero-btn"
			>
				Reserve a pack
			</a>
		</div>

		<div class="hero-tagline">
			<p><em>Bold like Davao. Smells like a story.</em></p>
		</div>
	</div>
</section>

<style>
	.hero-section {
		text-align: center;
		padding-top: 5rem;
		padding-bottom: 5rem;
		background: radial-gradient(circle at 50% 10%, var(--surface) 0%, var(--white) 70%);
	}

	.hero-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.brand-badge {
		display: inline-block;
		background-color: var(--blue-tint);
		color: var(--ink);
		font-size: 0.875rem;
		font-weight: 500;
		padding: 0.35rem 1rem;
		border-radius: var(--radius-pill);
		margin-bottom: 1.5rem;
	}

	.hero-title {
		max-width: 24ch;
		margin-bottom: 1.5rem;
	}

	.hero-subtitle {
		max-width: 48ch;
		font-size: clamp(1.125rem, 2vw, 1.35rem);
		color: var(--grey);
		margin-bottom: 2.25rem;
	}

	.hero-cta-wrapper {
		margin-bottom: 1.5rem;
	}

	.hero-btn {
		font-size: 1.125rem;
	}

	.hero-tagline {
		margin-top: 0.5rem;
	}

	.hero-tagline p {
		font-size: 0.95rem;
		color: var(--grey);
	}
</style>
