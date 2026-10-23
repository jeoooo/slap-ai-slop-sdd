<script lang="ts">
	import { Dialog } from '@ark-ui/svelte/dialog';
	import { Portal } from '@ark-ui/svelte/portal';

	export interface Product {
		id: string;
		name: string;
		description: string;
		price: string;
		roast: string;
		bestBrew: string;
		servingTip: string;
		accentColor: string; // CSS var name, e.g. 'var(--blue)'
		tintBg: string; // CSS var name, e.g. 'var(--blue-tint)'
	}

	interface Props {
		product: Product;
	}

	let { product }: Props = $props();
</script>

<article
	class="product-card"
	style="--card-accent: {product.accentColor};"
	aria-labelledby="product-title-{product.id}"
>
	<div class="product-top-bar" aria-hidden="true"></div>

	<div class="product-card-body">
		<div class="product-badge" style="background-color: {product.tintBg};">
			<span>{product.roast}</span>
		</div>

		<h3 id="product-title-{product.id}" class="product-name">
			{product.name}
		</h3>

		<p class="product-desc">
			{product.description}
		</p>

		<div class="product-price-row">
			<span class="product-price">{product.price}</span>
			<span class="product-unit">/ 250g pack</span>
		</div>

		<div class="product-action">
			<Dialog.Root id="dialog-{product.id}">
				<Dialog.Trigger class="btn btn-secondary product-details-btn">
					Details
				</Dialog.Trigger>

				<Portal>
				<Dialog.Backdrop />

				<Dialog.Positioner>
					<Dialog.Content>
						<Dialog.Title>{product.name} — Brew Notes</Dialog.Title>

						<Dialog.Description>
							<div class="dialog-notes">
								<div class="note-item">
									<strong class="note-label">Roast Profile:</strong>
									<span class="note-value">{product.roast}</span>
								</div>
								<div class="note-item">
									<strong class="note-label">Best Way to Brew:</strong>
									<span class="note-value">{product.bestBrew}</span>
								</div>
								<div class="note-item">
									<strong class="note-label">Serving Tip:</strong>
									<span class="note-value">{product.servingTip}</span>
								</div>
							</div>
						</Dialog.Description>

						<Dialog.CloseTrigger class="dialog-close-btn" aria-label="Close {product.name} details">
							<svg
								xmlns="http://www.w3.org/2000/svg"
								width="20"
								height="20"
								viewBox="0 0 24 24"
								fill="none"
								stroke="currentColor"
								stroke-width="2.5"
								stroke-linecap="round"
								stroke-linejoin="round"
								aria-hidden="true"
							>
								<line x1="18" y1="6" x2="6" y2="18"></line>
								<line x1="6" y1="6" x2="18" y2="18"></line>
							</svg>
						</Dialog.CloseTrigger>
					</Dialog.Content>
				</Dialog.Positioner>
				</Portal>
			</Dialog.Root>
		</div>
	</div>
</article>

<style>
	.product-card {
		display: flex;
		flex-direction: column;
		background-color: var(--white);
		border-radius: var(--radius-card);
		border: 1px solid rgba(32, 33, 36, 0.12);
		overflow: hidden;
		transition: transform 0.2s ease, box-shadow 0.2s ease;
		position: relative;
		height: 100%;
	}

	.product-card:hover {
		transform: translateY(-4px);
		box-shadow: 0 12px 24px rgba(32, 33, 36, 0.08);
	}

	.product-top-bar {
		height: 4px;
		width: 100%;
		background-color: var(--card-accent);
	}

	.product-card-body {
		padding: 2rem 1.75rem;
		display: flex;
		flex-direction: column;
		flex-grow: 1;
	}

	.product-badge {
		align-self: flex-start;
		color: var(--ink);
		font-size: 0.8125rem;
		font-weight: 500;
		padding: 0.25rem 0.75rem;
		border-radius: var(--radius-pill);
		margin-bottom: 1rem;
	}

	.product-name {
		font-size: 1.35rem;
		margin-bottom: 0.75rem;
		color: var(--ink);
	}

	.product-desc {
		color: var(--grey);
		font-size: 0.95rem;
		line-height: 1.5;
		margin-bottom: 1.5rem;
		flex-grow: 1;
	}

	.product-price-row {
		display: flex;
		align-items: baseline;
		gap: 0.375rem;
		margin-bottom: 1.5rem;
	}

	.product-price {
		font-size: 1.75rem;
		font-weight: 700;
		color: var(--ink);
	}

	.product-unit {
		font-size: 0.875rem;
		color: var(--grey);
	}

	.product-action {
		margin-top: auto;
	}

	:global(.product-details-btn) {
		width: 100%;
	}

	.dialog-notes {
		display: flex;
		flex-direction: column;
		gap: 1rem;
		margin-top: 1rem;
		text-align: left;
	}

	.note-item {
		display: flex;
		flex-direction: column;
		gap: 0.25rem;
	}

	.note-label {
		font-size: 0.875rem;
		font-weight: 600;
		color: var(--ink);
		text-transform: uppercase;
		letter-spacing: 0.04em;
	}

	.note-value {
		font-size: 1rem;
		color: var(--grey);
		line-height: 1.5;
	}
</style>
