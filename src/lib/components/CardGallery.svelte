<script lang="ts">
	import type { Picture } from 'vite-imagetools';

	type Props = {
		cards: Array<{
			src: Picture;
			name: string;
		}>;
	};

	let { cards }: Props = $props();
</script>

<div class="grid grid-cols-[repeat(auto-fill,minmax(220px,1fr))] gap-4 sm:gap-8">
	{#each cards as card (card.name)}
		<div
			class="flex flex-col items-center rounded-lg bg-gray-50 p-3 transition-all duration-300 ease-in-out hover:-translate-y-1 hover:shadow-xl"
		>
			<enhanced:img
				src={card.src}
				alt={card.name}
				class="size-full rounded-md object-cover"
				loading="lazy"
				decoding="async"
			/>
		</div>
	{/each}
</div>
