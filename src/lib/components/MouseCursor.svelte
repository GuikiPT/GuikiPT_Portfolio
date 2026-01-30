<script lang="ts">
	import { spring } from 'svelte/motion';
	import { onMount } from 'svelte';

	let coords1 = spring(
		{ x: 0, y: 0 },
		{
			stiffness: 0.05,
			damping: 0.25
		}
	);

	let coords2 = spring(
		{ x: 0, y: 0 },
		{
			stiffness: 0.1,
			damping: 0.35
		}
	);

	let size = spring(15);

	type TrailPoint = {
		x: number;
		y: number;
		opacity: number;
		id: number;
	};

	let trail: TrailPoint[] = $state([]);
	let trailId = 0;

	function addTrailPoint(x: number, y: number) {
		trail.push({ x, y, opacity: 0.8, id: trailId++ });
		if (trail.length > 40) {
			trail.shift();
		}
	}

	function updateTrail() {
		trail = trail
			.map((point) => ({
				...point,
				opacity: point.opacity - 0.02
			}))
			.filter((point) => point.opacity > 0);
	}

	let lastTime = Date.now();
	function animate() {
		const now = Date.now();
		if (now - lastTime > 16) {
			// ~60fps
			updateTrail();
			lastTime = now;
		}
		requestAnimationFrame(animate);
	}

	onMount(() => {
		animate();
	});
</script>

<svelte:window
	onmousemove={(e) => {
		coords1.set({ x: e.clientX, y: e.clientY });
		coords2.set({ x: e.clientX, y: e.clientY });
		addTrailPoint(e.clientX, e.clientY);
	}}
	onmousedown={() => {
		size.set(40);
	}}
	onmouseup={() => {
		size.set(15);
	}}
/>

<svg class="cursor-svg">
	{#if trail.length > 1}
		<path
			d={trail
				.map((point, i) => (i === 0 ? `M ${point.x} ${point.y}` : `L ${point.x} ${point.y}`))
				.join(' ')}
			stroke="#f97316"
			stroke-width="8"
			stroke-linecap="round"
			stroke-linejoin="round"
			fill="none"
			opacity={0.6}
			class="trail-line"
		/>
	{/if}
	<circle
		cx={$coords1.x}
		cy={$coords1.y}
		r={$size}
		stroke="#fb923c"
		stroke-width="2"
		fill-opacity="0"
		class="outer-circle"
	/>
	<circle cx={$coords2.x} cy={$coords2.y} r={$size / 4} fill="#f97316" class="inner-circle" />
</svg>

<style>
	:global(body) {
		cursor: none;
	}

	:global(a),
	:global(button),
	:global(input),
	:global(textarea),
	:global(select),
	:global([role='button']) {
		cursor: none !important;
	}

	.cursor-svg {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		pointer-events: none;
		z-index: 9999;
	}

	.trail-line {
		filter: blur(2px) drop-shadow(0 0 10px rgba(249, 115, 22, 0.6));
	}

	.outer-circle {
		filter: drop-shadow(0 0 8px rgba(249, 115, 22, 0.6));
	}

	.inner-circle {
		filter: drop-shadow(0 0 4px rgba(249, 115, 22, 0.8));
	}
</style>
