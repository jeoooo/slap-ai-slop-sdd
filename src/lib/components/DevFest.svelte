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

		<div class="devfest-socials" aria-label="GDG Davao social channels">
			<a
				href="https://www.facebook.com/gdgdavao"
				target="_blank"
				rel="noopener noreferrer"
				class="social-icon-btn"
				aria-label="GDG Davao on Facebook"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="20"
					height="20"
					viewBox="0 0 24 24"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"
					/>
				</svg>
			</a>

			<a
				href="https://github.com/gdgdavao"
				target="_blank"
				rel="noopener noreferrer"
				class="social-icon-btn"
				aria-label="GDG Davao on GitHub"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="20"
					height="20"
					viewBox="0 0 24 24"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"
					/>
				</svg>
			</a>

			<a
				href="https://www.linkedin.com/company/gdg-davao/"
				target="_blank"
				rel="noopener noreferrer"
				class="social-icon-btn"
				aria-label="GDG Davao on LinkedIn"
			>
				<svg
					xmlns="http://www.w3.org/2000/svg"
					width="20"
					height="20"
					viewBox="0 0 24 24"
					fill="currentColor"
					aria-hidden="true"
				>
					<path
						d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"
					/>
				</svg>
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

	.devfest-socials {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 1rem;
	}

	.social-icon-btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		width: 44px;
		height: 44px;
		border-radius: var(--radius-pill);
		color: var(--grey);
		background-color: var(--white);
		border: 1px solid rgba(32, 33, 36, 0.12);
		text-decoration: none;
		transition: color 0.15s ease, border-color 0.15s ease, transform 0.15s ease;
	}

	.social-icon-btn:hover {
		color: var(--blue-text);
		border-color: var(--blue-text);
		transform: translateY(-2px);
		opacity: 1;
	}
</style>
