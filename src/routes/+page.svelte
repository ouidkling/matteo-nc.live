<script lang="ts">
	import github from '$lib/assets/svg/github.svg';
	import linkedin from '$lib/assets/svg/linkedin.svg';
	import { onMount } from 'svelte';
	import { rainbow } from './rainbow.js';

	let canvas: HTMLCanvasElement;

	onMount(() => {
		const context = canvas.getContext('2d');

		let frame = requestAnimationFrame(function loop(t) {
			frame = requestAnimationFrame(loop);
			rainbow(context!, t);
		});

		return () => {
			cancelAnimationFrame(frame);
		};
	});
</script>

<canvas bind:this={canvas}></canvas>

<div class="flex flex-col justify-center items-center h-screen">
	<div>
		<h1 class="text">matteo-nc.live</h1>
	</div>
	<div class="flex">
		<a href="https://github.com/ouidkling" target="_blank" class="github logo">
			<img src={github} alt="github logo" />
		</a>
		<a href="https://linkedin.com/in/matteo-nc" target="_blank" class="linkedin logo">
			<img src={linkedin} alt="linkedin logo" />
		</a>
	</div>
</div>

<style lang="postcss">
	:global(html) {
		background-color: theme(colors.gray.100);
	}

	canvas {
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
	}

	.text {
		@apply text-4xl font-bold opacity-35;
	}

	.logo {
		@apply w-12 h-12 m-4 opacity-35;
	}
</style>
