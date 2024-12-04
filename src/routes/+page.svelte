<script>
	import Canvas from '$lib/Canvas.svelte';
	import Square from '$lib/Square.svelte';

	// we use a seeded random number generator to get consistent jitter
	let seed = 1;

	function random() {
		seed *= 16807;
		seed %= 2147483647;
		return (seed - 1) / 2147483646;
	}

	function jitter(amount) {
		return amount * (random() - 0.5);
	}
</script>

<main>
	<div class="container">
		<Canvas width={800} height={1200}>
			{#each Array(12) as _, c}
				{#each Array(22) as _, r}
					<Square
						x={180 + c * 40 + jitter(r * 2)}
						y={180 + r * 40 + jitter(r * 2)}
						size={40}
						rotate={jitter(r * 0.05)}
					/>
				{/each}
			{/each}
		</Canvas>
	</div>
</main>

<style>
	main {
		height: 90%; /* don't want to fill entire screen */
		/* MDN: Center with this code; better way? */
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}

	.container {
		height: 100%;
		aspect-ratio: 2 / 3;
		margin: 0 auto;
		background: rgb(224, 219, 213);
		filter: drop-shadow(1px 2px 3px hsl(211deg 11% 62% / 0.3))
			drop-shadow(2px 4px 6px hsl(211deg 11% 62% / 0.3))
			drop-shadow(4px 8px 12px hsl(211deg 11% 62% / 0.3));
		/* filter: drop-shadow(0.5em 0.5em 1em rgba(0, 0, 0, 0.4)); */
	}
</style>
