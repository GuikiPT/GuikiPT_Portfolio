<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
	import Navbar from '$lib/components/layout/Navbar.svelte';
	import MouseCursor from '$lib/components/MouseCursor.svelte';

	let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>

<MouseCursor />
<Navbar />

<main>
	{@render children()}
</main>
