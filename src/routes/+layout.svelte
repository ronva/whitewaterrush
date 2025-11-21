<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

{@render children()}

<!-- Decorative meandering river pattern -->
<div class="pointer-events-none fixed inset-0 -z-1">
	<svg viewBox="0 0 1200 800" preserveAspectRatio="none" class="size-full opacity-30">
		<!-- Main river path with meandering curves -->
		<path
			d="M-100,200 Q100,150 200,250 T400,200 Q500,300 600,250 T800,350 Q900,250 1000,300 T1200,250 L1200,0 L-100,0 Z"
			fill="currentColor"
			class="animate-river-flow text-river-blue/20 motion-reduce:animate-none"
		/>
		<!-- Secondary curves for depth -->
		<path
			d="M-100,280 Q150,220 250,320 T450,280 Q550,380 650,320 T850,420 Q950,320 1050,380 T1300,320 L1300,0 L-100,0 Z"
			fill="currentColor"
			class="animate-river-flow-slow text-river-blue/15 motion-reduce:animate-none"
		/>
		<!-- Tertiary curves for more depth -->
		<path
			d="M-100,350 Q200,280 300,400 T500,360 Q600,460 700,400 T900,500 Q1000,400 1100,460 T1400,420 L1400,0 L-100,0 Z"
			fill="currentColor"
			class="animate-river-flow-slower text-river-blue/10 motion-reduce:animate-none"
		/>
	</svg>
</div>
