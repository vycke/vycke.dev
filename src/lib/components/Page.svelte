<!-- src/component/PageTransitions.svelte -->
<script>
	import { description as _desc, title as _title } from '$lib/constants';

	import { fly } from 'svelte/transition';
	import Logo from './Logo.svelte';

	let styles = '';
	export { styles as class };
	export let title = _title;
	export let description = _desc;
	export let headerTitle = undefined;
</script>

<svelte:head>
	<title>{title} • Crinkles</title>
	<meta name="twitter:title" content={title} />
	<meta property="og:title" content={title} />

	<meta name="description" content={description} />
	<meta name="twitter:description" content={description} />
	<meta property="og:description" content={description} />
</svelte:head>

<div class="flex-grow text-0 relative">
	<header class="sticky post-0 center center-w-4 center-g-000 | mt-2 mb-0">
		<div class="flex-row items-center py-000 px-1">
			<Logo />
			{#if headerTitle}
				<h1 class="text-0 bold ml-1 monospace">/ {headerTitle}</h1>
			{/if}
		</div>
	</header>

	<main class={`center center-w-4 center-g-1 ${styles}`} in:fly={{ y: 50, duration: 250 }}>
		<slot />
	</main>
</div>

<style>
	.wrapper {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}

	header {
		z-index: 100;
		-webkit-backdrop-filter: blur(15px);
		backdrop-filter: blur(15px);
	}

	@supports not ((-webkit-backdrop-filter: none) or (backdrop-filter: none)) {
		header {
			background-color: var(--color-gray-400);
		}
	}
</style>
