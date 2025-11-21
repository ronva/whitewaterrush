<script lang="ts">
	import CardGallery from '$lib/components/CardGallery.svelte';
	import { onMount } from 'svelte';
	import advanceRiver from '$lib/assets/river-cards/advance river.png?enhanced';
	import brace from '$lib/assets/river-cards/brace.png?enhanced';
	import catchCurrent from '$lib/assets/river-cards/catch current.png?enhanced';
	import ferry from '$lib/assets/river-cards/ferry.png?enhanced';
	import paddle from '$lib/assets/river-cards/paddle.png?enhanced';
	import powerPaddle from '$lib/assets/river-cards/power paddle.png?enhanced';
	import readingWater from '$lib/assets/river-cards/reading water.png?enhanced';
	import recall from '$lib/assets/river-cards/recall.png?enhanced';
	import sculling from '$lib/assets/river-cards/sculling.png?enhanced';
	import spotHazard from '$lib/assets/river-cards/spot hazard.png?enhanced';

	const cards = [
		{ src: advanceRiver, name: 'Advance River' },
		{ src: brace, name: 'Brace' },
		{ src: catchCurrent, name: 'Catch Current' },
		{ src: ferry, name: 'Ferry' },
		{ src: paddle, name: 'Paddle' },
		{ src: powerPaddle, name: 'Power Paddle' },
		{ src: readingWater, name: 'Reading Water' },
		{ src: recall, name: 'Recall' },
		{ src: sculling, name: 'Sculling' },
		{ src: spotHazard, name: 'Spot Hazard' }
	];

	const TALLY_SCRIPT_URL = 'https://tally.so/widgets/embed.js';

	onMount(() => {
		const loadFeedbackForm = () => {
			// Load Tally embeds
			if (typeof window.Tally !== 'undefined') {
				window.Tally.loadEmbeds();
				return;
			}

			// Fallback if window.Tally is not available
			document
				.querySelectorAll<HTMLIFrameElement>('iframe[data-tally-src]:not([src])')
				.forEach((iframeEl) => {
					if (iframeEl.dataset.tallySrc) {
						iframeEl.src = iframeEl.dataset.tallySrc;
					}
				});
		};

		// If Tally is already loaded, load the embeds
		if (typeof window.Tally !== 'undefined') {
			loadFeedbackForm();
			return;
		}

		// If the Tally widget script is not loaded yet, load it
		if (document.querySelector(`script[src="${TALLY_SCRIPT_URL}"]`) === null) {
			const script = document.createElement('script');
			script.src = TALLY_SCRIPT_URL;
			script.onload = loadFeedbackForm;
			script.onerror = loadFeedbackForm;
			document.body.appendChild(script);
			return;
		}
	});
</script>

<main class="flex flex-col gap-24 px-4 py-16 sm:px-8 xl:pt-20">
	<!-- Hero Section -->
	<div
		class="mx-auto flex max-w-[1440px] items-start justify-center gap-8 max-xl:flex-col max-xl:items-center"
	>
		<div class="flex flex-col max-xl:items-center max-xl:text-center xl:flex-1">
			<h1
				class="mb-4 font-integral text-4xl font-black tracking-tight text-rapids-dark [font-style:oblique] sm:text-5xl lg:text-6xl"
			>
				Whitewater Rush
			</h1>
			<p class="mb-8 max-w-3xl text-lg text-pretty text-rapids-dark italic sm:text-2xl">
				Strategically position yourself and skillfully manage your speed as you avoid dangerous
				hazards and race to the finish line.
			</p>
			<div class="flex flex-col gap-4 sm:flex-row">
				<a
					href="/whitewater-rush-rulebook.pdf"
					target="_blank"
					rel="noopener noreferrer"
					class="flex items-center gap-2 rounded-lg bg-river-blue px-6 py-3 text-lg font-semibold text-white uppercase shadow-lg transition-all hover:bg-river-teal"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 576 512"
						class="size-5 fill-current"
						aria-label="PDF"
					>
						<path
							d="M208 48L96 48c-8.8 0-16 7.2-16 16l0 384c0 8.8 7.2 16 16 16l80 0 0 48-80 0c-35.3 0-64-28.7-64-64L32 64C32 28.7 60.7 0 96 0L229.5 0c17 0 33.3 6.7 45.3 18.7L397.3 141.3c12 12 18.7 28.3 18.7 45.3l0 149.5-48 0 0-128-88 0c-39.8 0-72-32.2-72-72l0-88zM348.1 160L256 67.9 256 136c0 13.3 10.7 24 24 24l68.1 0zM240 380l32 0c33.1 0 60 26.9 60 60s-26.9 60-60 60l-12 0 0 28c0 11-9 20-20 20s-20-9-20-20l0-128c0-11 9-20 20-20zm32 80c11 0 20-9 20-20s-9-20-20-20l-12 0 0 40 12 0zm96-80l32 0c28.7 0 52 23.3 52 52l0 64c0 28.7-23.3 52-52 52l-32 0c-11 0-20-9-20-20l0-128c0-11 9-20 20-20zm32 128c6.6 0 12-5.4 12-12l0-64c0-6.6-5.4-12-12-12l-12 0 0 88 12 0zm76-108c0-11 9-20 20-20l48 0c11 0 20 9 20 20s-9 20-20 20l-28 0 0 24 28 0c11 0 20 9 20 20s-9 20-20 20l-28 0 0 44c0 11-9 20-20 20s-20-9-20-20l0-128z"
						/>
					</svg>
					View Rulebook
				</a>
				<a
					href="#river-cards"
					class="flex items-center gap-2 rounded-lg border-2 border-rapids-dark bg-sand px-6 py-3 text-lg font-semibold text-rapids-dark uppercase shadow-lg transition-all hover:bg-sand/80"
				>
					<svg
						xmlns="http://www.w3.org/2000/svg"
						viewBox="0 0 512 512"
						class="size-5 fill-current"
						aria-label="Cards"
					>
						<path
							d="M448 32C483.3 32 512 60.65 512 96V416C512 451.3 483.3 480 448 480H64C28.65 480 0 451.3 0 416V96C0 60.65 28.65 32 64 32H448zM96 96C78.33 96 64 110.3 64 128C64 145.7 78.33 160 96 160H416C433.7 160 448 145.7 448 128C448 110.3 433.7 96 416 96H96zM416 224H96C78.33 224 64 238.3 64 256C64 273.7 78.33 288 96 288H416C433.7 288 448 273.7 448 256C448 238.3 433.7 224 416 224zM416 352H96C78.33 352 64 366.3 64 384C64 401.7 78.33 416 96 416H416C433.7 416 448 401.7 448 384C448 366.3 433.7 352 416 352z"
						/>
					</svg>
					View Card Gallery
				</a>
			</div>
		</div>

		<!-- Feedback Form Section -->
		<div class="max-w-xl shrink-0 rounded-2xl bg-white/75 py-4 shadow-lg backdrop-blur sm:py-6">
			<div class="px-4 pb-4 sm:px-6">
				<h2 class="mb-3 font-integral text-3xl font-bold text-rapids-dark sm:text-4xl">
					Share Your Feedback
				</h2>
				<p class="text-lg text-river-teal">
					Thank you for playtesting Whitewater Rush! I would love to get your feedback.
				</p>
			</div>

			<div class="h-150 overflow-y-auto overscroll-contain px-4 sm:px-6">
				<!-- Tally Form Embed -->
				<iframe
					data-tally-src="https://tally.so/embed/GxxyOo?alignLeft=1&hideTitle=1&transparentBackground=1&dynamicHeight=1"
					loading="lazy"
					width="100%"
					height="216"
					frameborder="0"
					marginheight="0"
					marginwidth="0"
					title="Share Your Feedback"
					class="block"
				></iframe>
			</div>
		</div>
	</div>

	{@render divider()}

	<div class="flex flex-col items-center gap-8">
		<h2 id="river-cards" class="font-integral text-3xl font-bold text-rapids-dark sm:text-4xl">
			River Cards
		</h2>
		<div class="mx-auto max-w-7xl">
			<CardGallery {cards} />
		</div>
	</div>

	{@render divider()}
</main>

{#snippet divider()}
	<svg
		viewBox="0 0 1200 120"
		preserveAspectRatio="none"
		class="h-16 w-full sm:h-20"
		aria-hidden="true"
	>
		<path
			d="M0,60 Q150,20 300,60 T600,60 T900,60 T1200,60"
			fill="none"
			stroke="currentColor"
			stroke-width="3"
			class="text-river-blue opacity-50"
		/>
	</svg>
{/snippet}
