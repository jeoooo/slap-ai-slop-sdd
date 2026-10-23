<script lang="ts">
</script>

<section class="section section-surface devfest-section" aria-labelledby="devfest-title">
	<div class="container devfest-container">
		<div class="brand-dots" aria-hidden="true">
			<span class="brand-dot dot-blue"></span>
			<span class="brand-dot dot-red"></span>
			<span class="brand-dot dot-yellow"></span>
			<span class="brand-dot dot-green"></span>
		</div>

		<img
			class="devfest-banner"
			src="/devfest-banner.webp"
			alt="DevFest Davao 2026 banner by Google Developer Group Davao: Build, Secure, Scale: Developers and Builders in the Agentic Era."
			width="1600"
			height="406"
			loading="lazy"
		/>

		<div class="devfest-chip">
			<span>Coming soon · November 2026</span>
		</div>

		<h2 id="devfest-title" class="devfest-title">
			DevFest Davao 2026
		</h2>

		<p class="devfest-desc">
			Registration is now officially open! Join the premier community tech gathering in the Davao region this November 2026.
		</p>

		<div class="devfest-action">
			<a
				href="https://apohub.gdgdavao.org/e/devfest-davao-2026"
				target="_blank"
				rel="noopener noreferrer"
				class="btn btn-secondary devfest-btn"
			>
				Register now
			</a>
		</div>

	</div>
</section>

<style>
	.devfest-section {
		text-align: center;
		border-top: 1px solid rgba(32, 33, 36, 0.08);
		border-bottom: 1px solid rgba(32, 33, 36, 0.08);
		padding-top: 4.5rem;
		padding-bottom: 4.5rem;
	}

	.devfest-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.devfest-banner {
		display: block;
		width: 100%;
		max-width: 56rem;
		height: auto;
		border-radius: var(--radius-card);
		margin-bottom: 1.5rem;
	}

	.devfest-chip {
		display: inline-block;
		background-color: var(--yellow-tint);
		color: var(--ink);
		font-size: 0.8125rem;
		font-weight: 600;
		padding: 0.3rem 0.875rem;
		border-radius: var(--radius-pill);
		margin-bottom: 1.25rem;
	}

	.devfest-title {
		margin-bottom: 0.75rem;
		color: var(--ink);
	}

	.devfest-desc {
		max-width: 44ch;
		color: var(--grey);
		font-size: 1.05rem;
		margin-bottom: 2rem;
	}

	.devfest-action {
		margin-bottom: 2rem;
	}

	.devfest-btn {
		min-width: 160px;
	}
</style>
