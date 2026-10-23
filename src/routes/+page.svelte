<script lang="ts">
	import { Accordion } from '@ark-ui/svelte/accordion';
	import { Tabs } from '@ark-ui/svelte/tabs';
	import { Dialog } from '@ark-ui/svelte/dialog';
	import { Portal } from '@ark-ui/svelte/portal';

	// State using Svelte 5 runes
	let isOrderOpen = $state(false);
	let selectedBlend = $state('Mt. Apo Signature Blend');
	let selectedGrind = $state('Whole Bean (Peak Freshness)');
	let quantity = $state(1);
	let orderPlaced = $state(false);
	let orderReference = $state('');

	// Interactive Quiz / Recommender State
	let userExperience = $state<'first-timer' | 'curious' | 'durian-lover'>('curious');
	let userBrewMethod = $state<'pour-over' | 'espresso' | 'cold-brew'>('pour-over');

	// Customer order form inputs
	let customerName = $state('');
	let customerEmail = $state('');
	let customerPhone = $state('');
	let shippingAddress = $state('');

	const products = [
		{
			id: 'apo-signature',
			name: 'Mt. Apo Signature Blend',
			tagline: 'The Flagship Davao Fusion',
			description:
				'Medium-dark roast Mt. Apo Arabica infused with Grade-A Davao Puyat durian pulp. Silky custard mouthfeel with lingering notes of dark toffee and toasted macadamia.',
			price: 590,
			size: '250g Valve Pouch',
			roast: 'Medium-Dark Roast',
			elevation: '1,420m MASL',
			durianLevel: 'Balanced Custard (4/5)',
			badge: 'Bestseller'
		},
		{
			id: 'midnight-espresso',
			name: 'Midnight Davao Espresso',
			tagline: 'Bold Volcanic Roast & Durian Nectar',
			description:
				'Highland Arabica & Robusta micro-lot roasted dark, glazed with slow-dehydrated Puyat durian nectar and Mindanao tablea cacao nibs. Thick crema with a decadent, creamy finish.',
			price: 620,
			size: '250g Valve Pouch',
			roast: 'Dark Espresso Roast',
			elevation: '1,350m MASL',
			durianLevel: 'Caramelized & Intense (3.5/5)',
			badge: 'Barista Choice'
		},
		{
			id: 'cold-brew-reserve',
			name: 'Davao Cold Brew Reserve',
			tagline: 'Slow Steeped Tropical Velvet',
			description:
				'Coarse-milled heirloom beans infused with fresh Arancillo and Puyat durian essence. Engineered for 18-hour cold immersion to create an ultra-smooth, buttery, low-acid nectar.',
			price: 650,
			size: '300g Coarse Grind Pouch',
			roast: 'Medium Cold Brew Roast',
			elevation: '1,500m MASL',
			durianLevel: 'Floral & Sweet (4.5/5)',
			badge: 'Limited Harvest'
		},
		{
			id: 'trio-gift-vault',
			name: 'Mindanao Heritage Tasting Trio',
			tagline: 'The Complete Davao Durian Coffee Experience',
			description:
				'Includes 150g each of our Mt. Apo Signature, Midnight Davao Espresso, and Cold Brew Reserve, presented in an artisanal handwoven Mindanao rattan gift canister with wooden scoop.',
			price: 1450,
			size: '3 x 150g Set',
			roast: 'Multi-Roast Flight',
			elevation: '1,350m – 1,500m MASL',
			durianLevel: 'All Profiles Included',
			badge: 'Gift Edition'
		}
	];

	function openOrderModal(blendName?: string) {
		if (blendName) {
			selectedBlend = blendName;
		}
		orderPlaced = false;
		isOrderOpen = true;
	}

	function handleOrderSubmit(e: SubmitEvent) {
		e.preventDefault();
		orderReference = 'APO-' + Math.floor(100000 + Math.random() * 900000);
		orderPlaced = true;
	}

	const unitPrice = $derived.by(() => {
		const match = products.find((p) => p.name === selectedBlend);
		return match ? match.price : 590;
	});

	const totalPrice = $derived(unitPrice * quantity);

	const recommendation = $derived.by(() => {
		if (userExperience === 'first-timer') {
			if (userBrewMethod === 'cold-brew') {
				return {
					blend: 'Davao Cold Brew Reserve',
					reason:
						'The cold steep mellows the aroma while keeping the sweetness silky and ultra-refreshing for first-time tasters.'
				};
			}
			return {
				blend: 'Midnight Davao Espresso',
				reason:
					'The dark cacao and caramel notes gently balance the durian sweetness, making it a delightfully accessible introduction.'
			};
		} else if (userExperience === 'durian-lover') {
			return {
				blend: 'Mt. Apo Signature Blend',
				reason:
					'Delivers the authentic, velvety richness of peak-harvest Davao Puyat durian combined with floral Mt. Apo highland Arabica.'
			};
		} else {
			return {
				blend:
					userBrewMethod === 'espresso'
						? 'Midnight Davao Espresso'
						: userBrewMethod === 'cold-brew'
							? 'Davao Cold Brew Reserve'
							: 'Mt. Apo Signature Blend',
				reason:
					'An exquisite harmony of bold single-origin coffee body and natural custard fruit finish.'
			};
		}
	});
</script>

<svelte:head>
	<title>Apo Royale — Davao Durian Specialty Coffee</title>
</svelte:head>

<!-- Top Announcement Banner -->
<div class="announcement-banner">
	<div class="announcement-content">
		<span class="pulse-dot"></span>
		<span class="announcement-text">
			<strong>Fresh Roast Alert:</strong> New harvest micro-batch from Mount Apo foothills, Davao
			City. Free shipping nationwide for orders ₱1,500+
		</span>
	</div>
</div>

<!-- Navigation Header -->
<header class="site-header">
	<div class="header-inner">
		<a href="#hero" class="brand-logo">
			<span class="logo-emblem">
				<svg viewBox="0 0 32 32" fill="none" class="emblem-svg">
					<path
						d="M16 2L20.5 9.5L29 11L22.5 17.5L24 26L16 21.5L8 26L9.5 17.5L3 11L11.5 9.5L16 2Z"
						fill="url(#durianGold)"
					/>
					<circle cx="16" cy="18" r="5" fill="#160f0a" />
					<path
						d="M16 15C17.6569 15 19 16.3431 19 18C19 19.6569 17.6569 21 16 21C14.3431 21 13 19.6569 13 18C13 16.3431 14.3431 15 16 15Z"
						fill="#f2a93b"
					/>
					<defs>
						<linearGradient id="durianGold" x1="3" y1="2" x2="29" y2="26" gradientUnits="userSpaceOnUse">
							<stop stop-color="#FFD700" />
							<stop offset="0.5" stop-color="#F2A93B" />
							<stop offset="1" stop-color="#B87714" />
						</linearGradient>
					</defs>
				</svg>
			</span>
			<div class="brand-text">
				<span class="brand-title">APO ROYALE</span>
				<span class="brand-sub">DAVAO DURIAN COFFEE</span>
			</div>
		</a>

		<nav class="desktop-nav" aria-label="Main Navigation">
			<a href="#flavor-profile">Flavor Profile</a>
			<a href="#blends">Our Blends</a>
			<a href="#deep-dive">The Craft</a>
			<a href="#recommender">Find Your Roast</a>
			<a href="#faq">FAQ</a>
		</nav>

		<div class="header-action">
			<button class="btn btn-primary" onclick={() => openOrderModal()}>
				<span>Reserve Batch</span>
				<svg
					width="16"
					height="16"
					viewBox="0 0 24 24"
					fill="none"
					stroke="currentColor"
					stroke-width="2"
					stroke-linecap="round"
					stroke-linejoin="round"
				>
					<path d="M5 12h14"></path>
					<path d="m12 5 7 7-7 7"></path>
				</svg>
			</button>
		</div>
	</div>
</header>

<main>
	<!-- Hero Section -->
	<section id="hero" class="hero-section">
		<div class="hero-backdrop-glow"></div>
		<div class="container hero-container">
			<div class="hero-content">
				<div class="hero-pill-badge">
					<span class="badge-icon">🌋</span>
					<span>Mount Apo Volcanic Terroir • 1,420m MASL</span>
				</div>

				<h1 class="hero-title">
					The King of Fruits.<br />
					<span class="gold-gradient-text">Meets the Craft of Coffee.</span>
				</h1>

				<p class="hero-subtitle">
					Handcrafted in Davao City. Single-origin highland Arabica slow-roasted to dark cocoa perfection,
					then micro-infused with the velvety, custard-sweet richness of authentic Davao Puyat durian.
					A legendary Philippine delicacy in every brew.
				</p>

				<div class="hero-cta-group">
					<button class="btn btn-primary btn-lg" onclick={() => openOrderModal()}>
						<span>Order Fresh Roast — ₱590</span>
						<svg
							width="18"
							height="18"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2.2"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<path d="M6 2 3 6v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2V6l-3-4Z" />
							<path d="M3 6h18" />
							<path d="M16 10a4 4 0 0 1-8 0" />
						</svg>
					</button>

					<a href="#flavor-profile" class="btn btn-outline btn-lg">
						<span>Explore Tasting Notes</span>
						<svg
							width="16"
							height="16"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<path d="m6 9 6 6 6-6" />
						</svg>
					</a>
				</div>

				<div class="hero-trust-indicators">
					<div class="trust-item">
						<div class="trust-stars">★★★★★</div>
						<div class="trust-text">4.9/5 from 1,400+ Davao Artisans</div>
					</div>
					<div class="trust-divider"></div>
					<div class="trust-item">
						<div class="trust-tag">100% Real Fruit</div>
						<div class="trust-text">Zero Artificial Syrups or Flavors</div>
					</div>
					<div class="trust-divider"></div>
					<div class="trust-item">
						<div class="trust-tag">Direct Trade</div>
						<div class="trust-text">Supporting Davao & Mt. Apo Farmers</div>
					</div>
				</div>
			</div>

			<!-- Visual Illustration Hero Card -->
			<div class="hero-visual">
				<div class="cup-showcase-card">
					<div class="card-glow-bg"></div>

					<!-- Artistic SVG representation of Durian Coffee Experience -->
					<div class="coffee-art-wrapper">
						<svg
							viewBox="0 0 400 400"
							fill="none"
							xmlns="http://www.w3.org/2000/svg"
							class="coffee-hero-illustration"
						>
							<!-- Volcanic Mountain Contour Background -->
							<path
								d="M20 320L130 180L200 240L310 130L380 320Z"
								fill="#22170f"
								opacity="0.4"
							/>
							<path
								d="M80 320L180 200L250 260L330 170L390 320Z"
								fill="#2a1d13"
								opacity="0.5"
							/>

							<!-- Floating Durian Star Blossom Petals -->
							<g class="floating-petals">
								<circle cx="90" cy="110" r="16" fill="#F2A93B" opacity="0.25" />
								<circle cx="320" cy="80" r="12" fill="#FFE89E" opacity="0.3" />
								<circle cx="350" cy="220" r="20" fill="#F2A93B" opacity="0.2" />
							</g>

							<!-- Steam Wisps -->
							<path
								d="M170 140C165 110 190 95 180 70"
								stroke="#FFE89E"
								stroke-width="3"
								stroke-linecap="round"
								opacity="0.7"
								class="steam-line-1"
							/>
							<path
								d="M200 135C205 105 185 85 200 60"
								stroke="#F2A93B"
								stroke-width="3.5"
								stroke-linecap="round"
								opacity="0.8"
								class="steam-line-2"
							/>
							<path
								d="M230 145C220 115 240 95 225 70"
								stroke="#FFE89E"
								stroke-width="3"
								stroke-linecap="round"
								opacity="0.6"
								class="steam-line-3"
							/>

							<!-- Coffee Cup Saucer -->
							<ellipse cx="200" cy="300" rx="140" ry="24" fill="#1b120b" />
							<ellipse cx="200" cy="296" rx="136" ry="20" stroke="#F2A93B" stroke-width="2" opacity="0.4" />

							<!-- Cup Body -->
							<path
								d="M100 180C100 265 140 280 200 280C260 280 300 265 300 180H100Z"
								fill="url(#cupGradient)"
							/>
							<!-- Cup Handle -->
							<path
								d="M300 195C330 195 340 245 300 255"
								stroke="#3a2517"
								stroke-width="14"
								stroke-linecap="round"
							/>
							<path
								d="M300 195C330 195 340 245 300 255"
								stroke="#F2A93B"
								stroke-width="3"
								stroke-linecap="round"
								opacity="0.6"
							/>

							<!-- Cup Rim / Crema Surface -->
							<ellipse cx="200" cy="180" rx="100" ry="24" fill="#2d1c10" stroke="#4a311f" stroke-width="3" />
							<!-- Velvety Durian Coffee Crema Swirl -->
							<ellipse cx="200" cy="180" rx="92" ry="20" fill="url(#cremaGradient)" />

							<!-- Durian Pattern Latte Art / Spikes in Crema -->
							<path
								d="M160 178C180 166 220 166 240 178C220 190 180 190 160 178Z"
								fill="#fae4b5"
								opacity="0.95"
							/>
							<path
								d="M185 168L200 188L215 168"
								stroke="#7a4613"
								stroke-width="2.5"
								stroke-linecap="round"
							/>
							<circle cx="200" cy="178" r="4" fill="#b87714" />

							<defs>
								<linearGradient id="cupGradient" x1="100" y1="180" x2="300" y2="280" gradientUnits="userSpaceOnUse">
									<stop stop-color="#2c1d13" />
									<stop offset="0.7" stop-color="#180e08" />
									<stop offset="1" stop-color="#0f0804" />
								</linearGradient>
								<linearGradient id="cremaGradient" x1="108" y1="180" x2="292" y2="180" gradientUnits="userSpaceOnUse">
									<stop stop-color="#B87714" />
									<stop offset="0.35" stop-color="#E59866" />
									<stop offset="0.65" stop-color="#F2A93B" />
									<stop offset="1" stop-color="#8C5312" />
								</linearGradient>
							</defs>
						</svg>
					</div>

					<!-- Floating Info Badges on visual -->
					<div class="floating-card top-left">
						<span class="floating-icon">🍈</span>
						<div>
							<div class="card-caption">Pure Pulp Infusion</div>
							<div class="card-title-sm">Davao Puyat Variety</div>
						</div>
					</div>

					<div class="floating-card bottom-right">
						<span class="floating-icon">☕</span>
						<div>
							<div class="card-caption">Tasting Note</div>
							<div class="card-title-sm">Custard Cream & Cocoa</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Sensory Flavor Profile Section -->
	<section id="flavor-profile" class="section-py sensory-section">
		<div class="container">
			<div class="section-header text-center">
				<span class="section-label">A Symphony on the Palate</span>
				<h2 class="section-title">Why Durian & Coffee Belong Together</h2>
				<p class="section-description">
					Many wonder how the pungent "King of Fruits" translates into coffee. Ripe Davao Puyat durian
					carries natural buttery lipids and rich fruit sugars. When met with the warmth of dark roasted
					Arabica, the pungent sulfur compounds convert into warm, caramelized toffee, roasted hazelnut,
					and thick custard cream.
				</p>
			</div>

			<div class="sensory-grid">
				<div class="sensory-metrics-card">
					<h3 class="card-heading">Flavor Intensity Matrix</h3>
					<p class="card-subtext">Measured by certified Q-graders & Mindanao coffee tasters</p>

					<div class="metric-bars">
						<div class="metric-row">
							<div class="metric-label">
								<span>Custard Creaminess & Body</span>
								<strong class="gold-text">9.6 / 10</strong>
							</div>
							<div class="metric-track">
								<div class="metric-fill" style="width: 96%"></div>
							</div>
						</div>

						<div class="metric-row">
							<div class="metric-label">
								<span>Caramel & Dark Cocoa Warmth</span>
								<strong class="gold-text">8.8 / 10</strong>
							</div>
							<div class="metric-track">
								<div class="metric-fill" style="width: 88%"></div>
							</div>
						</div>

						<div class="metric-row">
							<div class="metric-label">
								<span>Durian Aromatics (Floral & Sweet)</span>
								<strong class="gold-text">8.2 / 10</strong>
							</div>
							<div class="metric-track">
								<div class="metric-fill" style="width: 82%"></div>
							</div>
						</div>

						<div class="metric-row">
							<div class="metric-label">
								<span>Acidity (Low, Soft & Gentle)</span>
								<strong class="gold-text">3.2 / 10</strong>
							</div>
							<div class="metric-track">
								<div class="metric-fill" style="width: 32%"></div>
							</div>
						</div>

						<div class="metric-row">
							<div class="metric-label">
								<span>Velvety Sweet Lingering Finish</span>
								<strong class="gold-text">9.2 / 10</strong>
							</div>
							<div class="metric-track">
								<div class="metric-fill" style="width: 92%"></div>
							</div>
						</div>
					</div>

					<div class="flavor-tags">
						<span class="tag">#PuyatCustard</span>
						<span class="tag">#ToastedMacadamia</span>
						<span class="tag">#DarkMindanaoTablea</span>
						<span class="tag">#MtApoVolcanic</span>
						<span class="tag">#SilkyMouthfeel</span>
					</div>
				</div>

				<div class="sensory-notes-breakdown">
					<div class="note-box">
						<div class="note-icon-wrap">🍈</div>
						<div>
							<h4 class="note-heading">The Front Palate: Creamy Custard</h4>
							<p class="note-body">
								From the very first sip, you are greeted with a luxurious, velvety richness
								resembling a delicate crème brûlée or warm flan. Zero harsh acid bite.
							</p>
						</div>
					</div>

					<div class="note-box">
						<div class="note-icon-wrap">☕</div>
						<div>
							<h4 class="note-heading">The Mid Palate: Mt. Apo Arabica</h4>
							<p class="note-body">
								The backbone of shade-grown volcanic beans grounds the cup with dark chocolate,
								roasted almonds, and toasted brown sugar.
							</p>
						</div>
					</div>

					<div class="note-box">
						<div class="note-icon-wrap">✨</div>
						<div>
							<h4 class="note-heading">The Finish: Exotic Floral Aroma</h4>
							<p class="note-body">
								A warm, sweet tropical bouquet lingers gently on the breath—intensely comforting,
								nostalgic of Davao’s heritage orchards during harvest month.
							</p>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Blends Showcase Section -->
	<section id="blends" class="section-py blends-section">
		<div class="container">
			<div class="section-header text-center">
				<span class="section-label">Small-Batch Davao Roastery</span>
				<h2 class="section-title">Select Your Signature Blend</h2>
				<p class="section-description">
					Roasted weekly in Davao City. Available in whole bean or precision-ground for your favorite
					brewer.
				</p>
			</div>

			<div class="products-grid">
				{#each products as product}
					<div class="product-card">
						<div class="product-badge-wrap">
							<span class="product-badge">{product.badge}</span>
							<span class="product-size">{product.size}</span>
						</div>

						<h3 class="product-name">{product.name}</h3>
						<p class="product-tagline">{product.tagline}</p>

						<p class="product-desc">{product.description}</p>

						<div class="product-specs">
							<div class="spec-row">
								<span class="spec-key">Roast Profile</span>
								<span class="spec-val">{product.roast}</span>
							</div>
							<div class="spec-row">
								<span class="spec-key">Origin Elevation</span>
								<span class="spec-val">{product.elevation}</span>
							</div>
							<div class="spec-row">
								<span class="spec-key">Durian Infusion</span>
								<span class="spec-val">{product.durianLevel}</span>
							</div>
						</div>

						<div class="product-footer">
							<div class="product-price">
								<span class="currency">₱</span>
								<span class="amount">{product.price.toLocaleString()}</span>
							</div>

							<button
								class="btn btn-primary btn-sm"
								onclick={() => openOrderModal(product.name)}
								aria-label={`Order ${product.name}`}
							>
								<span>Order Now</span>
								<svg
									width="14"
									height="14"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2.5"
								>
									<path d="M5 12h14"></path>
									<path d="m12 5 7 7-7 7"></path>
								</svg>
							</button>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</section>

	<!-- Ark UI Tabs Deep Dive Section -->
	<section id="deep-dive" class="section-py deep-dive-section">
		<div class="container">
			<div class="section-header text-center">
				<span class="section-label">Interactive Exploration</span>
				<h2 class="section-title">The Davao Heritage & Craft</h2>
				<p class="section-description">
					Discover the volcanic terroir of Mount Apo, our gentle micro-infusion technique, and barista
					brewing rituals powered by Ark UI components.
				</p>
			</div>

			<!-- Ark UI Tabs Root -->
			<div class="tabs-container">
				<Tabs.Root defaultValue="origin">
					<Tabs.List class="ark-tabs-list">
						<Tabs.Trigger value="origin" class="ark-tabs-trigger">
							<span class="tab-icon">🌋</span>
							<span>Mount Apo Terroir</span>
						</Tabs.Trigger>
						<Tabs.Trigger value="cultivar" class="ark-tabs-trigger">
							<span class="tab-icon">🍈</span>
							<span>The Puyat Cultivar</span>
						</Tabs.Trigger>
						<Tabs.Trigger value="process" class="ark-tabs-trigger">
							<span class="tab-icon">⚙️</span>
							<span>Micro-Infusion Craft</span>
						</Tabs.Trigger>
						<Tabs.Trigger value="rituals" class="ark-tabs-trigger">
							<span class="tab-icon">☕</span>
							<span>Brewing Rituals</span>
						</Tabs.Trigger>
					</Tabs.List>

					<!-- Tab 1: Mount Apo Terroir -->
					<Tabs.Content value="origin" class="ark-tabs-content">
						<div class="tab-content-grid">
							<div class="tab-text-col">
								<h3>Highland Volcanic Soil at 1,420m MASL</h3>
								<p>
									Mount Apo is the highest mountain peak in the Philippine archipelago (2,954 meters).
									The lower volcanic slopes in Davao Del Sur boast ultra-fertile, mineral-dense soil
									loaded with potassium, phosphorus, and organic loam.
								</p>
								<p>
									Our coffee cherries are grown under native canopy trees alongside wild fruit groves.
									The cool mountain fog slows cherry maturation, allowing dense sugars and complex,
									fruity aromatics to develop inside the bean.
								</p>
								<ul class="tab-points">
									<li><strong>Location:</strong> Bansalan & Toril slopes, Mt. Apo, Davao</li>
									<li><strong>Harvest Season:</strong> November through February</li>
									<li><strong>Farming Practice:</strong> Regenerative shade-grown polyculture</li>
								</ul>
							</div>
							<div class="tab-visual-col">
								<div class="stat-highlight-box">
									<div class="big-number">1,420m</div>
									<div class="stat-caption">Elevation where our Arabica cherries thrive</div>
								</div>
								<div class="stat-highlight-box">
									<div class="big-number">100%</div>
									<div class="stat-caption">Direct single-estate Davao origin</div>
								</div>
							</div>
						</div>
					</Tabs.Content>

					<!-- Tab 2: The Puyat Cultivar -->
					<Tabs.Content value="cultivar" class="ark-tabs-content">
						<div class="tab-content-grid">
							<div class="tab-text-col">
								<h3>The Golden Pearl of Davao: Puyat Durian</h3>
								<p>
									Not all durians are equal. While common native varieties can be fibrous and overly
									sharp, the famed <em>Davao Puyat</em> cultivar is renowned for its thick, deep
									yellow-orange custard flesh with exceptional creaminess and fine fiber.
								</p>
								<p>
									We source exclusively tree-ripened Puyat fruit from partner heritage farms in Calinan,
									Davao City. At peak ripeness, the fruit's sweetness reaches 30+ degrees Brix, offering
									the exact lipid profile needed to create an exquisite coffee emulsion.
								</p>
								<ul class="tab-points">
									<li><strong>Flesh:</strong> Golden custard, dense, silky butter mouthfeel</li>
									<li><strong>Aroma Profile:</strong> Warm caramel, vanilla cream, tropical flora</li>
									<li><strong>Harvest Ethics:</strong> Fallen ripe harvest only — never artificially ripened</li>
								</ul>
							</div>
							<div class="tab-visual-col">
								<div class="stat-highlight-box">
									<div class="big-number">30°+ Brix</div>
									<div class="stat-caption">Natural fruit sweetness in ripe Puyat pulp</div>
								</div>
								<div class="stat-highlight-box">
									<div class="big-number">0 g</div>
									<div class="stat-caption">Added refined sugar or artificial flavor extracts</div>
								</div>
							</div>
						</div>
					</Tabs.Content>

					<!-- Tab 3: Micro-Infusion Process -->
					<Tabs.Content value="process" class="ark-tabs-content">
						<div class="tab-content-grid">
							<div class="tab-text-col">
								<h3>Precision Cryo-Milling & Micro-Tumbling</h3>
								<p>
									Traditional flavored coffees use chemical artificial oils that leave a bitter aftertaste.
									Apo Royale uses a proprietary 3-stage artisanal infusion:
								</p>
								<ol class="tab-steps-list">
									<li>
										<strong>Cryogenic Dehydration:</strong> Ripe Davao Puyat durian pulp is snap-frozen
										and freeze-dried at -40°C to lock in delicate aromatic volatile terpenes and natural
										creamy fats.
									</li>
									<li>
										<strong>Micro-Mesh Pulverization:</strong> The dehydrated fruit is milled into a
										microscopic golden velvet powder.
									</li>
									<li>
										<strong>Post-Roast Degassing Infusion:</strong> While freshly roasted Mt. Apo beans
										are in their peak porous degassing window, they are gently tumbled with the durian
										essence, drinking the natural fruit oils directly into the cellular pores of the bean.
									</li>
								</ol>
							</div>
							<div class="tab-visual-col">
								<div class="feature-card">
									<div class="feature-icon">❄️</div>
									<h4>Cryogenic Cold Lock</h4>
									<p>Preserves all volatile fruit aromatics without heat degradation</p>
								</div>
								<div class="feature-card">
									<div class="feature-icon">🛡️</div>
									<h4>Nitrogen Valve Pouch</h4>
									<p>Prevents oxidation and keeps beans bursting with fresh aroma for 6 months</p>
								</div>
							</div>
						</div>
					</Tabs.Content>

					<!-- Tab 4: Brewing Rituals -->
					<Tabs.Content value="rituals" class="ark-tabs-content">
						<div class="recipes-grid">
							<div class="recipe-card">
								<div class="recipe-badge">Pour-Over / V60</div>
								<h4>The Highland Drip Ritual</h4>
								<p class="recipe-desc">Highlights the floral, honeyed undertones of the blend.</p>
								<div class="recipe-meta">
									<span><strong>Dose:</strong> 18g</span>
									<span><strong>Water:</strong> 270g (92°C)</span>
									<span><strong>Time:</strong> 2:45 min</span>
								</div>
								<p class="recipe-tip">
									<em>Tip: Bloom with 50g water for 40 seconds to release the sweet durian blossom bouquet.</em>
								</p>
							</div>

							<div class="recipe-card">
								<div class="recipe-badge">Stovetop / Moka Pot</div>
								<h4>The Davao Midnight Espresso</h4>
								<p class="recipe-desc">Produces a thick, velvety crema with intense dessert richness.</p>
								<div class="recipe-meta">
									<span><strong>Dose:</strong> Full basket</span>
									<span><strong>Water:</strong> Pre-heated water to safety valve</span>
								</div>
								<p class="recipe-tip">
									<em>Tip: Serve straight or fold with steamed oat milk for an unmatched Durian Cortado.</em>
								</p>
							</div>

							<div class="recipe-card">
								<div class="recipe-badge">Signature Iced Latte</div>
								<h4>The Kadayawan Iced Durian Latte</h4>
								<p class="recipe-desc">The crowd favorite during Davao City's Kadayawan festival.</p>
								<div class="recipe-meta">
									<span>60ml Double Shot</span>
									<span>150ml Coconut Oat Milk</span>
									<span>Generous ice</span>
								</div>
								<p class="recipe-tip">
									<em>Tip: Shake vigorously in a cocktail shaker for 15 seconds to create a thick froth.</em>
								</p>
							</div>
						</div>
					</Tabs.Content>
				</Tabs.Root>
			</div>
		</div>
	</section>

	<!-- Interactive Recommender Quiz -->
	<section id="recommender" class="section-py recommender-section">
		<div class="container">
			<div class="recommender-card">
				<div class="recommender-header">
					<span class="section-label">Interactive Selector</span>
					<h2 class="section-title-sm">Find Your Perfect Davao Roast</h2>
					<p>Answer two quick questions to get tailored recommendations from our Davao roaster.</p>
				</div>

				<div class="recommender-controls">
					<div class="control-group">
						<label class="control-label" for="exp-select">1. What is your experience with Durian?</label>
						<div class="option-buttons" id="exp-select">
							<button
								type="button"
								class="opt-btn"
								class:selected={userExperience === 'first-timer'}
								onclick={() => (userExperience = 'first-timer')}
							>
								🌱 Curious First-Timer
							</button>
							<button
								type="button"
								class="opt-btn"
								class:selected={userExperience === 'curious'}
								onclick={() => (userExperience = 'curious')}
							>
								☕ Coffee Adventurer
							</button>
							<button
								type="button"
								class="opt-btn"
								class:selected={userExperience === 'durian-lover'}
								onclick={() => (userExperience = 'durian-lover')}
							>
								👑 Die-Hard Durian Fan
							</button>
						</div>
					</div>

					<div class="control-group">
						<label class="control-label" for="brew-select">2. How do you usually brew at home?</label>
						<div class="option-buttons" id="brew-select">
							<button
								type="button"
								class="opt-btn"
								class:selected={userBrewMethod === 'pour-over'}
								onclick={() => (userBrewMethod = 'pour-over')}
							>
								💧 Pour-Over / Drip
							</button>
							<button
								type="button"
								class="opt-btn"
								class:selected={userBrewMethod === 'espresso'}
								onclick={() => (userBrewMethod = 'espresso')}
							>
								⚡ Espresso / Moka Pot
							</button>
							<button
								type="button"
								class="opt-btn"
								class:selected={userBrewMethod === 'cold-brew'}
								onclick={() => (userBrewMethod = 'cold-brew')}
							>
								🧊 Iced / Cold Brew
							</button>
						</div>
					</div>
				</div>

				<!-- Live Recommended Result -->
				<div class="recommender-result">
					<div class="result-badge">Roaster's Match For You</div>
					<h3 class="result-title">{recommendation.blend}</h3>
					<p class="result-reason">{recommendation.reason}</p>
					<button
						class="btn btn-primary"
						onclick={() => openOrderModal(recommendation.blend)}
					>
						<span>Order {recommendation.blend}</span>
						<svg
							width="16"
							height="16"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
						>
							<path d="M5 12h14"></path>
							<path d="m12 5 7 7-7 7"></path>
						</svg>
					</button>
				</div>
			</div>
		</div>
	</section>

	<!-- Customer Reviews & Social Proof -->
	<section class="section-py reviews-section">
		<div class="container">
			<div class="section-header text-center">
				<span class="section-label">Davaweño & Global Acclaim</span>
				<h2 class="section-title">Loved by Coffee Seekers</h2>
				<p class="section-description">
					Read candid reviews from specialty baristas, travel writers, and proud Mindanao locals.
				</p>
			</div>

			<div class="reviews-grid">
				<div class="review-card">
					<div class="review-stars">★★★★★</div>
					<p class="review-quote">
						"I was admittedly skeptical because raw durian can overpower an entire room. But this roast
						is sheer culinary wizardry. It tastes like a warm Crème Brûlée latte with a subtle toasted
						tropical nuance. No artificial flavor aftertaste whatsoever."
					</p>
					<div class="reviewer-meta">
						<div class="reviewer-avatar">MV</div>
						<div>
							<div class="reviewer-name">Marco Villanueva</div>
							<div class="reviewer-role">Specialty Barista, Davao City</div>
						</div>
					</div>
				</div>

				<div class="review-card">
					<div class="review-stars">★★★★★</div>
					<p class="review-quote">
						"We ordered the Heritage Tasting Trio shipped to Makati, Manila. The aroma upon unboxing was
						intoxicating—deep cacao and sweet butter custard. My French press brew tasted so creamy that
						none of us added any sugar or dairy."
					</p>
					<div class="reviewer-meta">
						<div class="reviewer-avatar">CL</div>
						<div>
							<div class="reviewer-name">Clarisse Lim</div>
							<div class="reviewer-role">Third-Wave Coffee Enthusiast, Manila</div>
						</div>
					</div>
				</div>

				<div class="review-card">
					<div class="review-stars">★★★★★</div>
					<p class="review-quote">
						"As a proud Dabaweña living in Cebu, this cup brings me straight back home to Mt. Apo and
						the Kadayawan fruit markets. Authentic Puyat durian sweetness paired with bold Arabica body.
						A masterpiece."
					</p>
					<div class="reviewer-meta">
						<div class="reviewer-avatar">RS</div>
						<div>
							<div class="reviewer-name">Rochelle Santos</div>
							<div class="reviewer-role">Verified Buyer, Cebu</div>
						</div>
					</div>
				</div>
			</div>
		</div>
	</section>

	<!-- Ark UI Accordion FAQ Section -->
	<section id="faq" class="section-py faq-section">
		<div class="container faq-container">
			<div class="section-header text-center">
				<span class="section-label">Questions & Answers</span>
				<h2 class="section-title">Frequently Asked Questions</h2>
				<p class="section-description">
					Everything you need to know about our sourcing, aroma, preparation, and nationwide delivery.
				</p>
			</div>

			<!-- Ark UI Accordion Root -->
			<div class="accordion-wrap">
				<Accordion.Root defaultValue={['item-1']} class="ark-accordion-root">
					<!-- FAQ Item 1 -->
					<Accordion.Item value="item-1" class="ark-accordion-item">
						<Accordion.ItemTrigger class="ark-accordion-trigger">
							<span class="faq-question">Does it smell overwhelmingly pungent like raw durian?</span>
							<span class="accordion-icon">
								<svg
									width="18"
									height="18"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<path d="m6 9 6 6 6-6" />
								</svg>
							</span>
						</Accordion.ItemTrigger>
						<Accordion.ItemContent class="ark-accordion-content">
							<div class="faq-answer">
								Not at all. The pungency of fresh durian comes from raw sulfur volatile compounds.
								During our careful cryogenic freeze-drying and post-roast coffee micro-tumbling,
								those compounds caramelize into sweet, nutty notes of roasted hazelnut, warm vanilla,
								and brown butter custard. Non-durian eaters frequently fall in love with it!
							</div>
						</Accordion.ItemContent>
					</Accordion.Item>

					<!-- FAQ Item 2 -->
					<Accordion.Item value="item-2" class="ark-accordion-item">
						<Accordion.ItemTrigger class="ark-accordion-trigger">
							<span class="faq-question">Which durian variety do you use, and why Davao?</span>
							<span class="accordion-icon">
								<svg
									width="18"
									height="18"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<path d="m6 9 6 6 6-6" />
								</svg>
							</span>
						</Accordion.ItemTrigger>
						<Accordion.ItemContent class="ark-accordion-content">
							<div class="faq-answer">
								We source exclusively Grade-A <em>Puyat</em> and selected <em>Arancillo</em> durians
								from heritage family orchards in Calinan and Toril, Davao City. Davao is the undisputed
								Durian Capital of the Philippines due to the nutrient-dense volcanic soil of Mount Apo
								and balanced typhoon-free rainfall, producing fruit with higher custard density and lower
								water content.
							</div>
						</Accordion.ItemContent>
					</Accordion.Item>

					<!-- FAQ Item 3 -->
					<Accordion.Item value="item-3" class="ark-accordion-item">
						<Accordion.ItemTrigger class="ark-accordion-trigger">
							<span class="faq-question">Are there artificial syrups or synthetic flavoring oils added?</span>
							<span class="accordion-icon">
								<svg
									width="18"
									height="18"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<path d="m6 9 6 6 6-6" />
								</svg>
							</span>
						</Accordion.ItemTrigger>
						<Accordion.ItemContent class="ark-accordion-content">
							<div class="faq-answer">
								Zero. We pride ourselves on 100% natural infusion. We use genuine ripe Davao Puyat
								durian pulp dehydrated cryogenically and micro-milled directly with single-origin
								Arabica and Robusta beans from Mount Apo. No artificial flavorings, chemicals, or refined
								sugars are ever introduced.
							</div>
						</Accordion.ItemContent>
					</Accordion.Item>

					<!-- FAQ Item 4 -->
					<Accordion.Item value="item-4" class="ark-accordion-item">
						<Accordion.ItemTrigger class="ark-accordion-trigger">
							<span class="faq-question">How should I brew and store this coffee?</span>
							<span class="accordion-icon">
								<svg
									width="18"
									height="18"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<path d="m6 9 6 6 6-6" />
								</svg>
							</span>
						</Accordion.ItemTrigger>
						<Accordion.ItemContent class="ark-accordion-content">
							<div class="faq-answer">
								It brews beautifully across all methods: Pour-Over (V60), French Press, AeroPress,
								Stovetop Moka Pot, or Cold Brew. Because of the natural fruit lipids, French Press and
								Espresso yield an exceptionally thick crema. Keep the bag sealed in our one-way valve
								airtight pouch at cool room temperature. Avoid refrigerating whole beans.
							</div>
						</Accordion.ItemContent>
					</Accordion.Item>

					<!-- FAQ Item 5 -->
					<Accordion.Item value="item-5" class="ark-accordion-item">
						<Accordion.ItemTrigger class="ark-accordion-trigger">
							<span class="faq-question">Do you ship nationwide across the Philippines?</span>
							<span class="accordion-icon">
								<svg
									width="18"
									height="18"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2"
									stroke-linecap="round"
									stroke-linejoin="round"
								>
									<path d="m6 9 6 6 6-6" />
								</svg>
							</span>
						</Accordion.ItemTrigger>
						<Accordion.ItemContent class="ark-accordion-content">
							<div class="faq-answer">
								Yes! We roast weekly in Davao City and ship nationwide via express couriers. Metro
								Davao deliveries arrive within 24–48 hours; Metro Manila and Luzon usually arrive in 3–5
								business days; Visayas in 2–4 days. Every bag is nitrogen-flushed with a degassing valve
								so it reaches you at the absolute peak of its degassing window.
							</div>
						</Accordion.ItemContent>
					</Accordion.Item>
				</Accordion.Root>
			</div>
		</div>
	</section>

	<!-- Call to Action Banner -->
	<section class="section-py cta-banner-section">
		<div class="container">
			<div class="cta-banner-box">
				<div class="cta-banner-content">
					<span class="badge-icon">✈️</span>
					<h2>Taste the Legend of Davao in Your Cup</h2>
					<p>
						Order your fresh batch of Mount Apo single-origin Arabica & Davao Puyat Durian coffee today.
						Each pouch is small-batch roasted and sealed at peak flavor.
					</p>
					<button class="btn btn-primary btn-lg" onclick={() => openOrderModal()}>
						<span>Reserve Your Fresh Roast — ₱590</span>
						<svg
							width="18"
							height="18"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2.2"
						>
							<path d="M5 12h14"></path>
							<path d="m12 5 7 7-7 7"></path>
						</svg>
					</button>
				</div>
			</div>
		</div>
	</section>
</main>

<!-- Footer -->
<footer class="site-footer">
	<div class="container footer-container">
		<div class="footer-top">
			<div class="footer-brand">
				<div class="footer-logo">
					<span class="logo-text">APO ROYALE</span>
					<span class="logo-sub">DAVAO SPECIALTY ROASTERS</span>
				</div>
				<p class="footer-bio">
					Crafted with pride in Davao City, Philippines. Celebrating the rich volcanic terroir of Mount Apo
					and the King of Fruits. Direct-trade coffee that empowers local Mindanao highland farmers.
				</p>
				<div class="origin-stamp">
					📍 Roastery & Tasting Room: Toril Highland District, Davao City, 8000 Philippines
				</div>
			</div>

			<div class="footer-links-group">
				<h4>Blends</h4>
				<ul>
					<li><a href="#blends" onclick={() => openOrderModal('Mt. Apo Signature Blend')}>Mt. Apo Signature</a></li>
					<li><a href="#blends" onclick={() => openOrderModal('Midnight Davao Espresso')}>Midnight Davao Espresso</a></li>
					<li><a href="#blends" onclick={() => openOrderModal('Davao Cold Brew Reserve')}>Cold Brew Reserve</a></li>
					<li><a href="#blends" onclick={() => openOrderModal('Mindanao Heritage Tasting Trio')}>Heritage Trio Gift Vault</a></li>
				</ul>
			</div>

			<div class="footer-links-group">
				<h4>Explore</h4>
				<ul>
					<li><a href="#flavor-profile">Flavor Profile</a></li>
					<li><a href="#deep-dive">Mount Apo Terroir</a></li>
					<li><a href="#deep-dive">Brewing Rituals</a></li>
					<li><a href="#faq">FAQ</a></li>
				</ul>
			</div>

			<div class="footer-links-group">
				<h4>Davao Guild</h4>
				<ul>
					<li><span class="footer-badge">Direct Trade Certified</span></li>
					<li><span class="footer-badge">Mindanao Coffee Council</span></li>
					<li><span class="footer-badge">Davao Fruit Association</span></li>
				</ul>
			</div>
		</div>

		<div class="footer-bottom">
			<p>© 2026 Apo Royale Davao Specialty Coffee. All rights reserved.</p>
			<div class="footer-tags">
				<span>Mindanao Single-Origin</span>
				<span>•</span>
				<span>Puyat Durian Infusion</span>
				<span>•</span>
				<span>Philippine Specialty Coffee</span>
			</div>
		</div>
	</div>
</footer>

<!-- Ark UI Dialog Order Modal -->
<Dialog.Root bind:open={isOrderOpen}>
	<Portal>
		<Dialog.Backdrop class="dialog-backdrop" />
		<Dialog.Positioner class="dialog-positioner">
			<Dialog.Content class="dialog-content">
				<div class="dialog-header">
					<div>
						<Dialog.Title class="dialog-title">
							{#if orderPlaced}
								Order Confirmed!
							{:else}
								Reserve Your Davao Fresh Batch
							{/if}
						</Dialog.Title>
						<Dialog.Description class="dialog-description">
							{#if orderPlaced}
								Your batch is queued for freshly roasted packaging in Davao City.
							{:else}
								Small-batch roasted on Mount Apo slopes. Select your preferred grind and delivery details.
							{/if}
						</Dialog.Description>
					</div>

					<Dialog.CloseTrigger class="dialog-close-btn" aria-label="Close dialog">
						<svg
							width="20"
							height="20"
							viewBox="0 0 24 24"
							fill="none"
							stroke="currentColor"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<path d="M18 6 6 18"></path>
							<path d="m6 6 12 12"></path>
						</svg>
					</Dialog.CloseTrigger>
				</div>

				{#if orderPlaced}
					<!-- Order Success State -->
					<div class="order-success-state">
						<div class="success-icon-wrap">🍈☕</div>
						<h3>Maraming Salamat! (Thank You!)</h3>
						<p class="order-ref-text">
							Order Reference: <strong>{orderReference}</strong>
						</p>
						<p class="order-summary-text">
							We have reserved <strong>{quantity}x {selectedBlend}</strong> ({selectedGrind}) for
							<strong>{customerName || 'our esteemed coffee friend'}</strong>.
						</p>
						<div class="success-notice">
							A confirmation text & email tracking link will be sent to <strong>{customerEmail || customerPhone || 'your contact'}</strong>. Fresh shipment departs our Davao City facility within 24–48 hours.
						</div>

						<button class="btn btn-primary" onclick={() => (isOrderOpen = false)}>
							Done
						</button>
					</div>
				{:else}
					<!-- Order Form -->
					<form onsubmit={handleOrderSubmit} class="order-form">
						<!-- Select Blend -->
						<div class="form-group">
							<label class="form-label" for="blend-select">Choose Davao Blend</label>
							<select id="blend-select" bind:value={selectedBlend} class="form-select">
								{#each products as p}
									<option value={p.name}>{p.name} — ₱{p.price.toLocaleString()} ({p.size})</option>
								{/each}
							</select>
						</div>

						<!-- Select Grind -->
						<div class="form-group">
							<label class="form-label" for="grind-select">Grind Specification</label>
							<select id="grind-select" bind:value={selectedGrind} class="form-select">
								<option value="Whole Bean (Peak Freshness)">Whole Bean (Recommended for grinders)</option>
								<option value="Medium Grind (Pour-Over / Drip)">Medium Grind (Pour-Over / Drip Machine)</option>
								<option value="Fine Grind (Espresso / Moka Pot)">Fine Grind (Espresso / Moka Pot)</option>
								<option value="Coarse Grind (French Press / Cold Brew)">Coarse Grind (French Press / Cold Brew)</option>
							</select>
						</div>

						<!-- Quantity & Price Summary -->
						<div class="form-row quantity-price-row">
							<div class="form-group">
								<label class="form-label" for="quantity-input">Quantity</label>
								<div class="quantity-picker">
									<button
										type="button"
										class="qty-btn"
										onclick={() => quantity > 1 && quantity--}
										aria-label="Decrease quantity"
									>
										-
									</button>
									<span class="qty-num">{quantity}</span>
									<button
										type="button"
										class="qty-btn"
										onclick={() => quantity++}
										aria-label="Increase quantity"
									>
										+
									</button>
								</div>
							</div>

							<div class="price-summary-box">
								<div class="price-label">Total Amount</div>
								<div class="total-amount">₱{totalPrice.toLocaleString()}</div>
								<div class="shipping-note">
									{totalPrice >= 1500 ? '🎉 Free Nationwide Delivery' : '+ Standard Express Shipping'}
								</div>
							</div>
						</div>

						<div class="form-divider"></div>

						<!-- Customer Info -->
						<div class="form-row">
							<div class="form-group">
								<label class="form-label" for="name-input">Full Name</label>
								<input
									id="name-input"
									type="text"
									required
									placeholder="Juan Dela Cruz"
									bind:value={customerName}
									class="form-input"
								/>
							</div>
							<div class="form-group">
								<label class="form-label" for="phone-input">Mobile Number (PH)</label>
								<input
									id="phone-input"
									type="tel"
									required
									placeholder="0917 123 4567"
									bind:value={customerPhone}
									class="form-input"
								/>
							</div>
						</div>

						<div class="form-group">
							<label class="form-label" for="email-input">Email Address</label>
							<input
								id="email-input"
								type="email"
								required
								placeholder="juan@example.com"
								bind:value={customerEmail}
								class="form-input"
							/>
						</div>

						<div class="form-group">
							<label class="form-label" for="address-input">Delivery Address in the Philippines</label>
							<textarea
								id="address-input"
								required
								rows={2}
								placeholder="House/Unit No., Street, Barangay, City/Municipality, Province, Postal Code"
								bind:value={shippingAddress}
								class="form-textarea"
							></textarea>
						</div>

						<div class="dialog-actions">
							<button type="submit" class="btn btn-primary btn-block">
								<span>Complete Davao Order — ₱{totalPrice.toLocaleString()}</span>
								<svg
									width="16"
									height="16"
									viewBox="0 0 24 24"
									fill="none"
									stroke="currentColor"
									stroke-width="2.5"
								>
									<path d="M5 12h14"></path>
									<path d="m12 5 7 7-7 7"></path>
								</svg>
							</button>
						</div>
					</form>
				{/if}
			</Dialog.Content>
		</Dialog.Positioner>
	</Portal>
</Dialog.Root>

<style>
	/* Layout & Container */
	.container {
		width: 100%;
		max-width: 1200px;
		margin: 0 auto;
		padding: 0 1.5rem;
	}

	.section-py {
		padding: 5.5rem 0;
	}

	.text-center {
		text-align: center;
	}

	/* Top Announcement Banner */
	.announcement-banner {
		background: linear-gradient(90deg, #1f140a 0%, #3a220e 50%, #1f140a 100%);
		border-bottom: 1px solid var(--color-border-subtle);
		padding: 0.6rem 1rem;
		font-size: 0.85rem;
		color: var(--color-durian-cream);
	}

	.announcement-content {
		display: flex;
		align-items: center;
		justify-content: center;
		gap: 0.6rem;
		max-width: 1200px;
		margin: 0 auto;
		text-align: center;
	}

	.pulse-dot {
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background-color: var(--color-gold-primary);
		box-shadow: 0 0 8px var(--color-gold-glow);
		animation: pulse 2s infinite;
	}

	@keyframes pulse {
		0%,
		100% {
			transform: scale(1);
			opacity: 1;
		}
		50% {
			transform: scale(1.4);
			opacity: 0.6;
		}
	}

	/* Site Header */
	.site-header {
		position: sticky;
		top: 0;
		z-index: 50;
		background: rgba(12, 8, 5, 0.88);
		backdrop-filter: blur(14px);
		border-bottom: 1px solid rgba(56, 39, 26, 0.6);
	}

	.header-inner {
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 72px;
		max-width: 1200px;
		margin: 0 auto;
		padding: 0 1.5rem;
	}

	.brand-logo {
		display: flex;
		align-items: center;
		gap: 0.75rem;
	}

	.logo-emblem {
		width: 36px;
		height: 36px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.emblem-svg {
		width: 100%;
		height: 100%;
		filter: drop-shadow(0 2px 8px rgba(242, 169, 59, 0.4));
	}

	.brand-text {
		display: flex;
		flex-direction: column;
	}

	.brand-title {
		font-family: var(--font-serif);
		font-size: 1.25rem;
		font-weight: 700;
		letter-spacing: 0.08em;
		color: var(--color-gold-primary);
		line-height: 1.1;
	}

	.brand-sub {
		font-size: 0.62rem;
		letter-spacing: 0.16em;
		color: var(--color-text-secondary);
		font-weight: 600;
	}

	.desktop-nav {
		display: flex;
		align-items: center;
		gap: 2rem;
	}

	.desktop-nav a {
		font-size: 0.92rem;
		font-weight: 500;
		color: var(--color-text-secondary);
		transition: color 0.2s ease;
	}

	.desktop-nav a:hover {
		color: var(--color-gold-primary);
	}

	/* Buttons */
	.btn {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: 0.5rem;
		padding: 0.65rem 1.4rem;
		border-radius: var(--radius-full);
		font-size: 0.92rem;
		font-weight: 600;
		transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
	}

	.btn-primary {
		background: linear-gradient(135deg, #f2a93b 0%, #d48316 100%);
		color: #0c0805;
		box-shadow: 0 4px 18px rgba(242, 169, 59, 0.35);
	}

	.btn-primary:hover {
		transform: translateY(-2px);
		box-shadow: 0 6px 24px rgba(242, 169, 59, 0.5);
		background: linear-gradient(135deg, #ffbc58 0%, #df8d1a 100%);
	}

	.btn-outline {
		border: 1px solid var(--color-border);
		color: var(--color-text-primary);
		background: rgba(28, 20, 13, 0.4);
	}

	.btn-outline:hover {
		border-color: var(--color-gold-primary);
		color: var(--color-gold-primary);
		background: rgba(242, 169, 59, 0.08);
		transform: translateY(-2px);
	}

	.btn-lg {
		padding: 0.85rem 1.8rem;
		font-size: 1.05rem;
	}

	.btn-sm {
		padding: 0.5rem 1rem;
		font-size: 0.85rem;
	}

	.btn-block {
		width: 100%;
		padding: 0.85rem;
	}

	/* Hero Section */
	.hero-section {
		position: relative;
		padding: 5rem 0 6rem;
		overflow: hidden;
	}

	.hero-backdrop-glow {
		position: absolute;
		top: -20%;
		left: 50%;
		transform: translateX(-50%);
		width: 800px;
		height: 500px;
		background: radial-gradient(circle, rgba(242, 169, 59, 0.12) 0%, rgba(12, 8, 5, 0) 70%);
		pointer-events: none;
	}

	.hero-container {
		display: grid;
		grid-template-columns: 1.15fr 0.85fr;
		gap: 3.5rem;
		align-items: center;
	}

	.hero-pill-badge {
		display: inline-flex;
		align-items: center;
		gap: 0.5rem;
		background: rgba(38, 27, 18, 0.8);
		border: 1px solid var(--color-border-gold);
		padding: 0.4rem 1rem;
		border-radius: var(--radius-full);
		font-size: 0.85rem;
		font-weight: 500;
		color: var(--color-durian-cream);
		margin-bottom: 1.5rem;
	}

	.hero-title {
		font-family: var(--font-serif);
		font-size: clamp(2.4rem, 5vw, 3.8rem);
		line-height: 1.12;
		font-weight: 700;
		margin-bottom: 1.5rem;
		letter-spacing: -0.02em;
	}

	.gold-gradient-text {
		background: linear-gradient(135deg, #ffe89e 0%, #f2a93b 50%, #b87714 100%);
		-webkit-background-clip: text;
		background-clip: text;
		-webkit-text-fill-color: transparent;
	}

	.hero-subtitle {
		font-size: 1.15rem;
		line-height: 1.7;
		color: var(--color-text-secondary);
		margin-bottom: 2.2rem;
		max-width: 600px;
	}

	.hero-cta-group {
		display: flex;
		flex-wrap: wrap;
		gap: 1.2rem;
		margin-bottom: 2.8rem;
	}

	.hero-trust-indicators {
		display: flex;
		align-items: center;
		gap: 1.5rem;
		padding-top: 1.5rem;
		border-top: 1px solid var(--color-border-subtle);
	}

	.trust-stars {
		color: var(--color-gold-primary);
		letter-spacing: 2px;
		font-size: 0.95rem;
	}

	.trust-text {
		font-size: 0.78rem;
		color: var(--color-text-secondary);
	}

	.trust-tag {
		font-weight: 600;
		font-size: 0.85rem;
		color: var(--color-durian-flesh);
	}

	.trust-divider {
		width: 1px;
		height: 28px;
		background-color: var(--color-border-subtle);
	}

	/* Hero Showcase Card */
	.cup-showcase-card {
		position: relative;
		background: radial-gradient(circle at 50% 50%, #20150d 0%, #130c07 100%);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-lg);
		padding: 2.5rem 1.5rem;
		box-shadow: var(--shadow-card);
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.card-glow-bg {
		position: absolute;
		inset: 10%;
		background: radial-gradient(circle, rgba(242, 169, 59, 0.15) 0%, transparent 70%);
		filter: blur(30px);
		pointer-events: none;
	}

	.coffee-art-wrapper {
		width: 100%;
		max-width: 360px;
	}

	.coffee-hero-illustration {
		width: 100%;
		height: auto;
		filter: drop-shadow(0 15px 30px rgba(0, 0, 0, 0.6));
	}

	.steam-line-1 {
		animation: steamFloat 4s ease-in-out infinite;
	}
	.steam-line-2 {
		animation: steamFloat 4s ease-in-out infinite 1s;
	}
	.steam-line-3 {
		animation: steamFloat 4s ease-in-out infinite 2s;
	}

	@keyframes steamFloat {
		0%,
		100% {
			transform: translateY(0) scaleY(1);
			opacity: 0.5;
		}
		50% {
			transform: translateY(-8px) scaleY(1.1);
			opacity: 0.9;
		}
	}

	.floating-card {
		position: absolute;
		display: flex;
		align-items: center;
		gap: 0.75rem;
		background: rgba(22, 15, 10, 0.92);
		border: 1px solid var(--color-border-gold);
		backdrop-filter: blur(10px);
		padding: 0.6rem 1rem;
		border-radius: var(--radius-md);
		box-shadow: 0 8px 24px rgba(0, 0, 0, 0.5);
	}

	.floating-card.top-left {
		top: 15px;
		left: -15px;
	}

	.floating-card.bottom-right {
		bottom: 15px;
		right: -15px;
	}

	.floating-icon {
		font-size: 1.4rem;
	}

	.card-caption {
		font-size: 0.7rem;
		text-transform: uppercase;
		letter-spacing: 0.08em;
		color: var(--color-text-secondary);
	}

	.card-title-sm {
		font-size: 0.88rem;
		font-weight: 700;
		color: var(--color-durian-cream);
	}

	/* Section Headers */
	.section-header {
		margin-bottom: 3.5rem;
	}

	.section-label {
		display: inline-block;
		text-transform: uppercase;
		letter-spacing: 0.16em;
		font-size: 0.8rem;
		font-weight: 700;
		color: var(--color-gold-primary);
		margin-bottom: 0.6rem;
	}

	.section-title {
		font-family: var(--font-serif);
		font-size: clamp(2rem, 3.5vw, 2.8rem);
		font-weight: 700;
		line-height: 1.2;
		margin-bottom: 1rem;
	}

	.section-description {
		max-width: 680px;
		margin: 0 auto;
		color: var(--color-text-secondary);
		font-size: 1.05rem;
		line-height: 1.7;
	}

	/* Sensory Flavor Profile Section */
	.sensory-section {
		background: linear-gradient(180deg, #0c0805 0%, #150e09 50%, #0c0805 100%);
	}

	.sensory-grid {
		display: grid;
		grid-template-columns: 1.1fr 0.9fr;
		gap: 3rem;
		align-items: center;
	}

	.sensory-metrics-card {
		background: var(--color-bg-card);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-lg);
		padding: 2.2rem;
		box-shadow: var(--shadow-subtle);
	}

	.card-heading {
		font-family: var(--font-serif);
		font-size: 1.4rem;
		margin-bottom: 0.3rem;
	}

	.card-subtext {
		font-size: 0.85rem;
		color: var(--color-text-secondary);
		margin-bottom: 1.8rem;
	}

	.metric-bars {
		display: flex;
		flex-direction: column;
		gap: 1.2rem;
		margin-bottom: 1.8rem;
	}

	.metric-label {
		display: flex;
		justify-content: space-between;
		font-size: 0.9rem;
		font-weight: 500;
		margin-bottom: 0.4rem;
	}

	.gold-text {
		color: var(--color-gold-primary);
	}

	.metric-track {
		height: 8px;
		background: #110b07;
		border-radius: 4px;
		overflow: hidden;
	}

	.metric-fill {
		height: 100%;
		background: linear-gradient(90deg, #d48316 0%, #f2a93b 100%);
		border-radius: 4px;
		box-shadow: 0 0 10px rgba(242, 169, 59, 0.4);
	}

	.flavor-tags {
		display: flex;
		flex-wrap: wrap;
		gap: 0.5rem;
		padding-top: 1.2rem;
		border-top: 1px solid var(--color-border-subtle);
	}

	.tag {
		font-size: 0.78rem;
		font-weight: 600;
		background: rgba(242, 169, 59, 0.1);
		color: var(--color-durian-cream);
		border: 1px solid rgba(242, 169, 59, 0.25);
		padding: 0.3rem 0.7rem;
		border-radius: var(--radius-full);
	}

	.sensory-notes-breakdown {
		display: flex;
		flex-direction: column;
		gap: 1.5rem;
	}

	.note-box {
		display: flex;
		gap: 1.2rem;
		background: var(--color-bg-elevated);
		border: 1px solid var(--color-border-subtle);
		padding: 1.5rem;
		border-radius: var(--radius-md);
		transition: transform 0.2s ease, border-color 0.2s ease;
	}

	.note-box:hover {
		transform: translateX(4px);
		border-color: var(--color-border-gold);
	}

	.note-icon-wrap {
		width: 48px;
		height: 48px;
		border-radius: var(--radius-sm);
		background: rgba(242, 169, 59, 0.12);
		border: 1px solid rgba(242, 169, 59, 0.25);
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 1.4rem;
		flex-shrink: 0;
	}

	.note-heading {
		font-size: 1.05rem;
		font-weight: 700;
		color: var(--color-durian-cream);
		margin-bottom: 0.3rem;
	}

	.note-body {
		font-size: 0.92rem;
		color: var(--color-text-secondary);
		line-height: 1.6;
	}

	/* Products Grid */
	.products-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
		gap: 1.8rem;
	}

	.product-card {
		background: var(--color-bg-card);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-lg);
		padding: 2rem 1.6rem;
		display: flex;
		flex-direction: column;
		transition: all 0.3s ease;
		position: relative;
	}

	.product-card:hover {
		transform: translateY(-6px);
		border-color: var(--color-border-gold);
		box-shadow: 0 16px 36px rgba(0, 0, 0, 0.6);
	}

	.product-badge-wrap {
		display: flex;
		justify-content: space-between;
		align-items: center;
		margin-bottom: 1.2rem;
	}

	.product-badge {
		font-size: 0.72rem;
		font-weight: 700;
		text-transform: uppercase;
		letter-spacing: 0.08em;
		background: var(--color-gold-primary);
		color: #0c0805;
		padding: 0.25rem 0.65rem;
		border-radius: var(--radius-full);
	}

	.product-size {
		font-size: 0.8rem;
		color: var(--color-text-secondary);
		font-weight: 500;
	}

	.product-name {
		font-family: var(--font-serif);
		font-size: 1.35rem;
		line-height: 1.25;
		margin-bottom: 0.3rem;
	}

	.product-tagline {
		font-size: 0.85rem;
		color: var(--color-gold-primary);
		font-weight: 500;
		margin-bottom: 1rem;
	}

	.product-desc {
		font-size: 0.88rem;
		color: var(--color-text-secondary);
		line-height: 1.6;
		margin-bottom: 1.5rem;
		flex-grow: 1;
	}

	.product-specs {
		display: flex;
		flex-direction: column;
		gap: 0.5rem;
		background: rgba(14, 9, 6, 0.6);
		padding: 0.9rem;
		border-radius: var(--radius-sm);
		border: 1px solid var(--color-border-subtle);
		margin-bottom: 1.5rem;
	}

	.spec-row {
		display: flex;
		justify-content: space-between;
		font-size: 0.78rem;
	}

	.spec-key {
		color: var(--color-text-tertiary);
	}

	.spec-val {
		font-weight: 600;
		color: var(--color-text-primary);
	}

	.product-footer {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding-top: 1rem;
		border-top: 1px solid var(--color-border-subtle);
	}

	.product-price {
		display: flex;
		align-items: baseline;
		gap: 0.2rem;
	}

	.product-price .currency {
		font-size: 1rem;
		color: var(--color-gold-primary);
		font-weight: 600;
	}

	.product-price .amount {
		font-size: 1.6rem;
		font-weight: 800;
		font-family: var(--font-sans);
		color: var(--color-text-primary);
	}

	/* Ark UI Tabs Styles */
	.tabs-container {
		background: var(--color-bg-card);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-lg);
		padding: 2rem;
		box-shadow: var(--shadow-card);
	}

	:global(.ark-tabs-list) {
		display: flex;
		flex-wrap: wrap;
		gap: 0.8rem;
		border-bottom: 1px solid var(--color-border-subtle);
		padding-bottom: 1.2rem;
		margin-bottom: 2rem;
	}

	:global(.ark-tabs-trigger) {
		display: inline-flex;
		align-items: center;
		gap: 0.5rem;
		padding: 0.65rem 1.2rem;
		border-radius: var(--radius-full);
		font-size: 0.92rem;
		font-weight: 600;
		color: var(--color-text-secondary);
		background: rgba(22, 15, 10, 0.6);
		border: 1px solid transparent;
		transition: all 0.2s ease;
	}

	:global(.ark-tabs-trigger:hover) {
		color: var(--color-text-primary);
		background: rgba(38, 27, 18, 0.6);
	}

	:global(.ark-tabs-trigger[data-selected]) {
		color: #0c0805;
		background: var(--color-gold-primary);
		border-color: var(--color-gold-primary);
		box-shadow: 0 4px 14px rgba(242, 169, 59, 0.35);
	}

	:global(.ark-tabs-content) {
		animation: fadeIn 0.3s ease;
	}

	@keyframes fadeIn {
		from {
			opacity: 0;
			transform: translateY(6px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.tab-content-grid {
		display: grid;
		grid-template-columns: 1.2fr 0.8fr;
		gap: 3rem;
		align-items: center;
	}

	.tab-text-col h3 {
		font-family: var(--font-serif);
		font-size: 1.7rem;
		margin-bottom: 1rem;
		color: var(--color-durian-cream);
	}

	.tab-text-col p {
		font-size: 0.98rem;
		color: var(--color-text-secondary);
		line-height: 1.7;
		margin-bottom: 1.2rem;
	}

	.tab-points {
		list-style: none;
		display: flex;
		flex-direction: column;
		gap: 0.6rem;
		margin-top: 1.2rem;
	}

	.tab-points li {
		font-size: 0.92rem;
		color: var(--color-text-primary);
	}

	.tab-points li strong {
		color: var(--color-gold-primary);
	}

	.tab-steps-list {
		padding-left: 1.2rem;
		display: flex;
		flex-direction: column;
		gap: 0.8rem;
		color: var(--color-text-secondary);
		font-size: 0.95rem;
		line-height: 1.6;
	}

	.tab-steps-list strong {
		color: var(--color-durian-cream);
	}

	.tab-visual-col {
		display: flex;
		flex-direction: column;
		gap: 1.5rem;
	}

	.stat-highlight-box {
		background: var(--color-bg-elevated);
		border: 1px solid var(--color-border);
		padding: 1.8rem;
		border-radius: var(--radius-md);
		text-align: center;
	}

	.big-number {
		font-family: var(--font-serif);
		font-size: 2.6rem;
		font-weight: 700;
		color: var(--color-gold-primary);
		line-height: 1;
		margin-bottom: 0.5rem;
	}

	.stat-caption {
		font-size: 0.88rem;
		color: var(--color-text-secondary);
	}

	.feature-card {
		background: var(--color-bg-elevated);
		border: 1px solid var(--color-border);
		padding: 1.4rem;
		border-radius: var(--radius-md);
	}

	.feature-icon {
		font-size: 1.6rem;
		margin-bottom: 0.5rem;
	}

	.feature-card h4 {
		font-size: 1.05rem;
		margin-bottom: 0.3rem;
		color: var(--color-durian-cream);
	}

	.feature-card p {
		font-size: 0.85rem;
		color: var(--color-text-secondary);
	}

	.recipes-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 1.5rem;
	}

	.recipe-card {
		background: var(--color-bg-elevated);
		border: 1px solid var(--color-border);
		padding: 1.6rem;
		border-radius: var(--radius-md);
	}

	.recipe-badge {
		display: inline-block;
		font-size: 0.72rem;
		font-weight: 700;
		color: var(--color-gold-primary);
		text-transform: uppercase;
		letter-spacing: 0.1em;
		margin-bottom: 0.6rem;
	}

	.recipe-card h4 {
		font-size: 1.2rem;
		margin-bottom: 0.4rem;
		color: var(--color-durian-cream);
	}

	.recipe-desc {
		font-size: 0.88rem;
		color: var(--color-text-secondary);
		margin-bottom: 1rem;
	}

	.recipe-meta {
		display: flex;
		flex-wrap: wrap;
		gap: 0.8rem;
		font-size: 0.82rem;
		color: var(--color-text-primary);
		background: rgba(12, 8, 5, 0.6);
		padding: 0.7rem;
		border-radius: var(--radius-sm);
		margin-bottom: 1rem;
	}

	.recipe-tip {
		font-size: 0.82rem;
		color: var(--color-text-secondary);
		display: block;
	}

	/* Recommender Section */
	.recommender-card {
		background: radial-gradient(circle at 50% 0%, #24180f 0%, #160f0a 100%);
		border: 1px solid var(--color-border-gold);
		border-radius: var(--radius-lg);
		padding: 3rem;
		box-shadow: var(--shadow-card);
	}

	.recommender-header {
		text-align: center;
		margin-bottom: 2.5rem;
	}

	.section-title-sm {
		font-family: var(--font-serif);
		font-size: 2rem;
		margin-bottom: 0.5rem;
	}

	.recommender-controls {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 2.5rem;
		margin-bottom: 2.5rem;
	}

	.control-group {
		display: flex;
		flex-direction: column;
		gap: 0.8rem;
	}

	.control-label {
		font-size: 0.95rem;
		font-weight: 600;
		color: var(--color-durian-cream);
	}

	.option-buttons {
		display: flex;
		flex-direction: column;
		gap: 0.6rem;
	}

	.opt-btn {
		text-align: left;
		padding: 0.8rem 1.2rem;
		border-radius: var(--radius-md);
		border: 1px solid var(--color-border);
		background: rgba(14, 9, 6, 0.6);
		color: var(--color-text-secondary);
		font-size: 0.92rem;
		font-weight: 500;
		transition: all 0.2s ease;
	}

	.opt-btn:hover {
		border-color: var(--color-gold-dark);
		color: var(--color-text-primary);
	}

	.opt-btn.selected {
		border-color: var(--color-gold-primary);
		background: rgba(242, 169, 59, 0.15);
		color: var(--color-durian-cream);
		box-shadow: 0 0 16px rgba(242, 169, 59, 0.2);
	}

	.recommender-result {
		background: rgba(10, 6, 4, 0.7);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-md);
		padding: 1.8rem;
		text-align: center;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 0.8rem;
	}

	.result-badge {
		font-size: 0.75rem;
		text-transform: uppercase;
		letter-spacing: 0.12em;
		font-weight: 700;
		color: var(--color-gold-primary);
	}

	.result-title {
		font-family: var(--font-serif);
		font-size: 1.6rem;
		color: var(--color-text-primary);
	}

	.result-reason {
		max-width: 600px;
		font-size: 0.95rem;
		color: var(--color-text-secondary);
		margin-bottom: 0.5rem;
	}

	/* Reviews Section */
	.reviews-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
		gap: 2rem;
	}

	.review-card {
		background: var(--color-bg-card);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-lg);
		padding: 2rem;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.review-stars {
		color: var(--color-gold-primary);
		letter-spacing: 3px;
		margin-bottom: 1rem;
	}

	.review-quote {
		font-size: 0.95rem;
		line-height: 1.7;
		color: var(--color-text-secondary);
		font-style: italic;
		margin-bottom: 1.5rem;
	}

	.reviewer-meta {
		display: flex;
		align-items: center;
		gap: 0.8rem;
		border-top: 1px solid var(--color-border-subtle);
		padding-top: 1rem;
	}

	.reviewer-avatar {
		width: 40px;
		height: 40px;
		border-radius: 50%;
		background: var(--color-border);
		color: var(--color-gold-primary);
		font-weight: 700;
		font-size: 0.85rem;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.reviewer-name {
		font-weight: 700;
		font-size: 0.92rem;
		color: var(--color-text-primary);
	}

	.reviewer-role {
		font-size: 0.78rem;
		color: var(--color-text-tertiary);
	}

	/* Ark UI Accordion FAQ */
	.faq-container {
		max-width: 860px;
	}

	:global(.ark-accordion-root) {
		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	:global(.ark-accordion-item) {
		background: var(--color-bg-card);
		border: 1px solid var(--color-border);
		border-radius: var(--radius-md);
		overflow: hidden;
		transition: border-color 0.2s ease;
	}

	:global(.ark-accordion-item:hover) {
		border-color: var(--color-border-gold);
	}

	:global(.ark-accordion-trigger) {
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 1.4rem 1.6rem;
		font-size: 1.05rem;
		font-weight: 600;
		color: var(--color-text-primary);
		text-align: left;
		cursor: pointer;
		background: none;
		border: none;
		transition: color 0.2s ease;
	}

	:global(.ark-accordion-trigger:hover) {
		color: var(--color-gold-primary);
	}

	:global(.ark-accordion-trigger[data-state='open'] .accordion-icon) {
		transform: rotate(180deg);
		color: var(--color-gold-primary);
	}

	.accordion-icon {
		display: flex;
		align-items: center;
		justify-content: center;
		transition: transform 0.25s cubic-bezier(0.16, 1, 0.3, 1);
		color: var(--color-text-secondary);
	}

	:global(.ark-accordion-content) {
		padding: 0 1.6rem 1.4rem 1.6rem;
		animation: expandAnim 0.25s cubic-bezier(0.16, 1, 0.3, 1);
	}

	@keyframes expandAnim {
		from {
			opacity: 0;
			transform: translateY(-6px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.faq-answer {
		font-size: 0.95rem;
		line-height: 1.7;
		color: var(--color-text-secondary);
	}

	/* CTA Banner Section */
	.cta-banner-box {
		background: linear-gradient(135deg, #2a1b10 0%, #150d08 100%);
		border: 1px solid var(--color-border-gold);
		border-radius: var(--radius-lg);
		padding: 4rem 2rem;
		text-align: center;
		box-shadow: var(--shadow-glow);
	}

	.cta-banner-content {
		max-width: 650px;
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1.2rem;
	}

	.cta-banner-content h2 {
		font-family: var(--font-serif);
		font-size: clamp(2rem, 3.5vw, 2.6rem);
		line-height: 1.2;
	}

	.cta-banner-content p {
		font-size: 1.05rem;
		color: var(--color-text-secondary);
		line-height: 1.7;
	}

	/* Footer */
	.site-footer {
		background: #080503;
		border-top: 1px solid var(--color-border-subtle);
		padding: 4.5rem 0 2.5rem;
	}

	.footer-top {
		display: grid;
		grid-template-columns: 1.8fr 1fr 1fr 1fr;
		gap: 3rem;
		margin-bottom: 3.5rem;
	}

	.footer-logo {
		display: flex;
		flex-direction: column;
		margin-bottom: 1rem;
	}

	.logo-text {
		font-family: var(--font-serif);
		font-size: 1.3rem;
		font-weight: 700;
		color: var(--color-gold-primary);
		letter-spacing: 0.08em;
	}

	.logo-sub {
		font-size: 0.65rem;
		letter-spacing: 0.16em;
		color: var(--color-text-secondary);
		font-weight: 600;
	}

	.footer-bio {
		font-size: 0.88rem;
		color: var(--color-text-secondary);
		line-height: 1.7;
		margin-bottom: 1rem;
	}

	.origin-stamp {
		font-size: 0.8rem;
		color: var(--color-text-tertiary);
	}

	.footer-links-group h4 {
		font-size: 0.95rem;
		font-weight: 700;
		color: var(--color-text-primary);
		margin-bottom: 1.2rem;
	}

	.footer-links-group ul {
		list-style: none;
		display: flex;
		flex-direction: column;
		gap: 0.7rem;
	}

	.footer-links-group a {
		font-size: 0.88rem;
		color: var(--color-text-secondary);
		transition: color 0.2s ease;
	}

	.footer-links-group a:hover {
		color: var(--color-gold-primary);
	}

	.footer-badge {
		display: inline-block;
		font-size: 0.75rem;
		padding: 0.2rem 0.6rem;
		background: rgba(38, 27, 18, 0.6);
		border: 1px solid var(--color-border-subtle);
		border-radius: var(--radius-sm);
		color: var(--color-durian-cream);
	}

	.footer-bottom {
		display: flex;
		justify-content: space-between;
		align-items: center;
		border-top: 1px solid var(--color-border-subtle);
		padding-top: 2rem;
		font-size: 0.82rem;
		color: var(--color-text-tertiary);
	}

	.footer-tags {
		display: flex;
		gap: 0.6rem;
	}

	/* Ark UI Dialog Modal Styles */
	:global(.dialog-backdrop) {
		position: fixed;
		inset: 0;
		background: rgba(0, 0, 0, 0.75);
		backdrop-filter: blur(8px);
		z-index: 100;
		animation: backdropFade 0.25s ease;
	}

	@keyframes backdropFade {
		from {
			opacity: 0;
		}
		to {
			opacity: 1;
		}
	}

	:global(.dialog-positioner) {
		position: fixed;
		inset: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		z-index: 101;
		padding: 1.5rem;
	}

	:global(.dialog-content) {
		background: #18110b;
		border: 1px solid var(--color-border-gold);
		border-radius: var(--radius-lg);
		width: 100%;
		max-width: 580px;
		max-height: 90vh;
		overflow-y: auto;
		padding: 2.2rem;
		box-shadow: 0 25px 60px rgba(0, 0, 0, 0.8);
		position: relative;
		animation: modalScale 0.25s cubic-bezier(0.16, 1, 0.3, 1);
	}

	@keyframes modalScale {
		from {
			opacity: 0;
			transform: scale(0.95) translateY(8px);
		}
		to {
			opacity: 1;
			transform: scale(1) translateY(0);
		}
	}

	.dialog-header {
		display: flex;
		justify-content: space-between;
		align-items: flex-start;
		margin-bottom: 1.8rem;
	}

	:global(.dialog-title) {
		font-family: var(--font-serif);
		font-size: 1.6rem;
		font-weight: 700;
		color: var(--color-durian-cream);
		line-height: 1.2;
		margin-bottom: 0.3rem;
	}

	:global(.dialog-description) {
		font-size: 0.88rem;
		color: var(--color-text-secondary);
	}

	:global(.dialog-close-btn) {
		background: rgba(255, 255, 255, 0.05);
		border: 1px solid var(--color-border);
		color: var(--color-text-secondary);
		border-radius: 50%;
		width: 34px;
		height: 34px;
		display: flex;
		align-items: center;
		justify-content: center;
		cursor: pointer;
		transition: all 0.2s ease;
		flex-shrink: 0;
	}

	:global(.dialog-close-btn:hover) {
		background: rgba(255, 255, 255, 0.1);
		color: var(--color-text-primary);
	}

	/* Form Elements */
	.order-form {
		display: flex;
		flex-direction: column;
		gap: 1.2rem;
	}

	.form-group {
		display: flex;
		flex-direction: column;
		gap: 0.4rem;
	}

	.form-row {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 1rem;
	}

	.form-label {
		font-size: 0.85rem;
		font-weight: 600;
		color: var(--color-durian-cream);
	}

	.form-input,
	.form-select,
	.form-textarea {
		background: #0f0a06;
		border: 1px solid var(--color-border);
		border-radius: var(--radius-sm);
		padding: 0.75rem 1rem;
		color: var(--color-text-primary);
		font-family: inherit;
		font-size: 0.92rem;
		outline: none;
		transition: border-color 0.2s ease;
		width: 100%;
	}

	.form-input:focus,
	.form-select:focus,
	.form-textarea:focus {
		border-color: var(--color-gold-primary);
		box-shadow: 0 0 0 3px rgba(242, 169, 59, 0.15);
	}

	.form-textarea {
		resize: vertical;
	}

	.quantity-picker {
		display: flex;
		align-items: center;
		background: #0f0a06;
		border: 1px solid var(--color-border);
		border-radius: var(--radius-sm);
		width: fit-content;
	}

	.qty-btn {
		width: 36px;
		height: 38px;
		display: flex;
		align-items: center;
		justify-content: center;
		font-size: 1.2rem;
		color: var(--color-text-secondary);
	}

	.qty-btn:hover {
		color: var(--color-gold-primary);
	}

	.qty-num {
		padding: 0 0.8rem;
		font-weight: 700;
		font-size: 1rem;
	}

	.price-summary-box {
		background: rgba(242, 169, 59, 0.08);
		border: 1px solid var(--color-border-gold);
		border-radius: var(--radius-sm);
		padding: 0.6rem 1rem;
		display: flex;
		flex-direction: column;
		justify-content: center;
	}

	.price-label {
		font-size: 0.72rem;
		text-transform: uppercase;
		letter-spacing: 0.08em;
		color: var(--color-text-secondary);
	}

	.total-amount {
		font-size: 1.4rem;
		font-weight: 800;
		color: var(--color-gold-primary);
		line-height: 1.1;
	}

	.shipping-note {
		font-size: 0.72rem;
		color: var(--color-durian-flesh);
		margin-top: 0.2rem;
	}

	.form-divider {
		height: 1px;
		background: var(--color-border-subtle);
		margin: 0.4rem 0;
	}

	.order-success-state {
		text-align: center;
		padding: 1.5rem 0;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1rem;
	}

	.success-icon-wrap {
		font-size: 3rem;
		margin-bottom: 0.5rem;
	}

	.order-ref-text {
		font-size: 1.1rem;
		color: var(--color-gold-primary);
	}

	.order-summary-text {
		font-size: 0.95rem;
		color: var(--color-text-secondary);
		max-width: 440px;
	}

	.success-notice {
		background: rgba(46, 139, 87, 0.15);
		border: 1px solid var(--color-leaf-emerald);
		border-radius: var(--radius-sm);
		padding: 0.9rem;
		font-size: 0.85rem;
		color: #a3e635;
		margin: 0.8rem 0;
		max-width: 460px;
	}

	/* Responsive Media Queries */
	@media (max-width: 960px) {
		.hero-container {
			grid-template-columns: 1fr;
			gap: 2.5rem;
		}

		.sensory-grid {
			grid-template-columns: 1fr;
		}

		.tab-content-grid {
			grid-template-columns: 1fr;
		}

		.recommender-controls {
			grid-template-columns: 1fr;
		}

		.footer-top {
			grid-template-columns: 1fr 1fr;
		}
	}

	@media (max-width: 680px) {
		.desktop-nav {
			display: none;
		}

		.form-row {
			grid-template-columns: 1fr;
		}

		.footer-top {
			grid-template-columns: 1fr;
		}

		.footer-bottom {
			flex-direction: column;
			gap: 1rem;
			text-align: center;
		}

		.hero-trust-indicators {
			flex-direction: column;
			align-items: flex-start;
			gap: 1rem;
		}

		.trust-divider {
			display: none;
		}
	}
</style>
