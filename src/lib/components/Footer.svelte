<script lang="ts">
	const currentYear = new Date().getFullYear();
</script>

<footer class="footer-section" aria-labelledby="footer-title">
	<div class="container footer-container">
		<h2 id="footer-title" class="sr-only">Duriano Coffee Footer</h2>

		<div class="footer-top">
			<div class="footer-brand">
				<div class="brand-dots" aria-hidden="true">
					<span class="brand-dot dot-blue"></span>
					<span class="brand-dot dot-red"></span>
					<span class="brand-dot dot-yellow"></span>
					<span class="brand-dot dot-green"></span>
				</div>
				<span class="footer-brand-name">Duriano Coffee</span>
				<p class="footer-tagline">Bold like Davao. Smells like a story.</p>
			</div>

			<div class="footer-contact">
				<strong class="footer-heading">Roastery & Tasting Room</strong>
				<address class="footer-address">
					Unit 4B, Durian Highlands Plaza<br />
					Mount Apo View St., Bajada<br />
					Davao City 8000, Philippines
				</address>
				<p class="footer-email">
					<a href="mailto:hello@durianocoffee.demo">hello@durianocoffee.demo</a>
				</p>
			</div>

			<div class="footer-social-section">
				<strong class="footer-heading">Connect (Placeholders)</strong>
				<ul class="footer-social-list" aria-label="Social media placeholders">
					<li>
						<a href="#instagram" class="footer-social-link">Instagram</a>
					</li>
					<li>
						<a href="#twitter" class="footer-social-link">X / Twitter</a>
					</li>
					<li>
						<a href="#tiktok" class="footer-social-link">TikTok</a>
					</li>
				</ul>
			</div>
		</div>

		<div class="footer-bottom">
			<div class="footer-disclaimers">
				<p class="disclaimer-line">Demo site, not a real business.</p>
				<p class="disclaimer-line">Google-inspired theme, not affiliated with Google.</p>
			</div>
			<p class="footer-copy">
				© {currentYear} Duriano Coffee Demo. All rights reserved.
			</p>
		</div>
	</div>
</footer>

<style>
	.footer-section {
		background-color: var(--ink);
		color: var(--white);
		padding-top: 4rem;
		padding-bottom: 3rem;
		border-top: 1px solid rgba(255, 255, 255, 0.1);
	}

	.footer-container {
		display: flex;
		flex-direction: column;
		gap: 3rem;
	}

	.footer-top {
		display: grid;
		grid-template-columns: 1fr;
		gap: 2.5rem;
	}

	@media (min-width: 768px) {
		.footer-top {
			grid-template-columns: 1.5fr 1fr 1fr;
			gap: 3rem;
		}
	}

	.footer-brand {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	.footer-brand-name {
		font-size: 1.35rem;
		font-weight: 700;
		color: var(--white);
	}

	.footer-tagline {
		font-size: 0.95rem;
		color: #BDC1C6;
	}

	.footer-heading {
		display: block;
		font-size: 0.875rem;
		font-weight: 600;
		color: var(--white);
		text-transform: uppercase;
		letter-spacing: 0.05em;
		margin-bottom: 0.75rem;
	}

	.footer-address {
		font-style: normal;
		font-size: 0.95rem;
		line-height: 1.6;
		color: #BDC1C6;
		margin-bottom: 0.5rem;
	}

	.footer-email a {
		color: #8AB4F8;
		text-decoration: underline;
		font-size: 0.95rem;
	}

	.footer-social-list {
		list-style: none;
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	.footer-social-link {
		color: #8AB4F8;
		display: inline-flex;
		align-items: center;
		min-height: 44px;
		text-decoration: underline;
		font-size: 0.95rem;
	}

	.footer-social-link:hover {
		color: var(--white);
	}

	.footer-bottom {
		border-top: 1px solid rgba(255, 255, 255, 0.12);
		padding-top: 2rem;
		display: flex;
		flex-direction: column;
		gap: 1rem;
		font-size: 0.875rem;
		color: #9AA0A6;
	}

	@media (min-width: 768px) {
		.footer-bottom {
			flex-direction: row;
			justify-content: space-between;
			align-items: center;
		}
	}

	.footer-disclaimers {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
	}

	.disclaimer-line {
		color: #BDC1C6;
		font-size: 0.875rem;
		margin: 0;
	}

	.footer-copy {
		color: #9AA0A6;
		font-size: 0.8125rem;
		margin: 0;
	}
</style>
