<script lang="ts">
	import { Accordion } from '@ark-ui/svelte/accordion';

	interface Step {
		id: string;
		num: string;
		title: string;
		summary: string;
		tint: string;
	}

	const steps: Step[] = [
		{
			id: 'brew',
			num: '1',
			title: 'Brew slowly with hot, fresh water',
			summary:
				'Use water just off the boil (around 90°C–93°C). Pour evenly over the grounds to gently release both the roasted coffee oils and the delicate durian sweetness without scalding.',
			tint: 'var(--blue-tint)'
		},
		{
			id: 'add-milk',
			num: '2',
			title: 'Add milk or drink it straight',
			summary:
				'Duriano is naturally silky. Drinking it black reveals crisp caramelized durian aroma. Adding a splash of oat milk, whole milk, or sweetened condensed milk transforms it into an unforgettably luscious custard latte.',
			tint: 'var(--yellow-tint)'
		},
		{
			id: 'sip',
			num: '3',
			title: 'Sip, breathe, and embrace the story',
			summary:
				'Take in the aroma before your first sip. Notice how the initial punch mellows into chocolate, hazelnut, and sweet tropical fruit. You are drinking a true Davao original.',
			tint: 'var(--green-tint)'
		}
	];

	let activeValue = $state(['brew']);
</script>

<section class="section section-surface how-to-section" aria-labelledby="how-to-title">
	<div class="container">
		<div class="how-to-header">
			<div class="brand-dots" aria-hidden="true">
				<span class="brand-dot dot-yellow"></span>
				<span class="brand-dot dot-green"></span>
			</div>
			<h2 id="how-to-title" class="how-to-title">How to enjoy it</h2>
			<p class="how-to-intro">
				Whether you brew with a French press, pour-over, or quick sachet, here is how to get the most out of every cup.
			</p>
		</div>

		<div class="how-to-content">
			<Accordion.Root
				value={activeValue}
				onValueChange={(details) => (activeValue = details.value)}
				collapsible
				class="how-to-accordion"
			>
				{#each steps as step (step.id)}
					<Accordion.Item value={step.id}>
						<Accordion.ItemTrigger>
							<div class="trigger-left">
								<span class="step-num-circle" style="background-color: {step.tint};">
									{step.num}
								</span>
								<span class="step-title-text">{step.title}</span>
							</div>

							<Accordion.ItemIndicator>
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
									<polyline points="6 9 12 15 18 9"></polyline>
								</svg>
							</Accordion.ItemIndicator>
						</Accordion.ItemTrigger>

						<Accordion.ItemContent>
							<p class="step-content-text">{step.summary}</p>
						</Accordion.ItemContent>
					</Accordion.Item>
				{/each}
			</Accordion.Root>

			<div class="first-timer-tip">
				<div class="tip-badge">
					<span>Tip for first-timers</span>
				</div>
				<h3 class="tip-heading">Do not fear the initial aroma</h3>
				<p class="tip-text">
					Fresh durian is famously pungent, but the hot roast softens the sulfur notes into warm tropical custard and honeyed cacao. Let the cup cool for two minutes before judging—the flavor opens up magnificently as the temperature settles.
				</p>
			</div>
		</div>
	</div>
</section>

<style>
	.how-to-section {
		border-top: 1px solid rgba(32, 33, 36, 0.08);
		border-bottom: 1px solid rgba(32, 33, 36, 0.08);
	}

	.how-to-header {
		margin-bottom: 3rem;
		max-width: 44rem;
	}

	.how-to-title {
		margin-bottom: 0.75rem;
	}

	.how-to-intro {
		color: var(--grey);
		font-size: 1.125rem;
	}

	.how-to-content {
		display: grid;
		grid-template-columns: 1fr;
		gap: 3rem;
		align-items: start;
	}

	@media (min-width: 900px) {
		.how-to-content {
			grid-template-columns: 1.2fr 0.8fr;
			gap: 4rem;
		}
	}

	.trigger-left {
		display: flex;
		align-items: center;
		gap: 1rem;
	}

	.step-num-circle {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		width: 2rem;
		height: 2rem;
		border-radius: var(--radius-pill);
		font-size: 0.875rem;
		font-weight: 700;
		color: var(--ink);
		flex-shrink: 0;
	}

	.step-title-text {
		font-size: 1.125rem;
		font-weight: 600;
		color: var(--ink);
	}

	.step-content-text {
		color: var(--grey);
		line-height: 1.6;
		margin: 0;
	}

	.first-timer-tip {
		background-color: var(--white);
		border-radius: var(--radius-card);
		padding: 2rem;
		border: 1px solid rgba(32, 33, 36, 0.1);
		box-shadow: 0 4px 16px rgba(32, 33, 36, 0.04);
	}

	.tip-badge {
		display: inline-block;
		background-color: var(--yellow-tint);
		color: var(--ink);
		font-size: 0.8125rem;
		font-weight: 600;
		padding: 0.25rem 0.75rem;
		border-radius: var(--radius-pill);
		margin-bottom: 1rem;
	}

	.tip-heading {
		font-size: 1.25rem;
		color: var(--ink);
		margin-bottom: 0.75rem;
	}

	.tip-text {
		color: var(--grey);
		line-height: 1.6;
		font-size: 0.95rem;
	}
</style>
