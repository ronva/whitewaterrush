<script lang="ts">
	import { onMount } from 'svelte';

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

<main
	class="relative isolate mx-auto flex min-h-screen max-w-[1440px] items-center justify-center gap-8 px-4 py-16 max-xl:flex-col sm:px-8 xl:items-start xl:pt-20"
>
	<!-- Hero Section -->
	<div class="flex flex-col items-start max-xl:items-center max-xl:text-center xl:flex-1">
		<h1
			class="mb-4 font-integral text-4xl font-black tracking-tight text-rapids-dark [font-style:oblique] sm:text-5xl lg:text-6xl"
		>
			Whitewater Rush
		</h1>
		<p class="mb-8 max-w-3xl text-lg text-pretty text-rapids-dark italic sm:text-2xl">
			Strategically position yourself and skillfully manage your speed as you avoid dangerous
			hazards and race to the finish line.
		</p>
		<a
			href="/whitewater-rush-rulebook.pdf"
			target="_blank"
			rel="noopener noreferrer"
			class="flex items-center gap-2 rounded-lg bg-river-blue px-8 py-3 text-lg font-semibold text-white uppercase shadow-lg transition-all hover:bg-river-teal"
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

		<div class="max-h-150 overflow-y-auto overscroll-contain px-4 sm:px-6">
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
</main>
