<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
</script>

<svelte:head>
	<title>Rock Paper Scissors - SvelteKit</title>

	<link rel="icon" href={favicon} />
</svelte:head>

<!-- <div class="flex min-h-screen flex-col bg-radial-[at_50%_0%] from-[#1f3757] to-[#131537] font-sans"> -->
<div class="bg-gradient-1 flex min-h-screen flex-col font-sans">
	{@render children()}
</div>
