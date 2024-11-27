<script lang="ts">
	import '../app.postcss';
	import Navigation from '$lib/Navigation/Navigation.svelte';
	import {
		initializeStores,
		Drawer,
		getDrawerStore,
		LightSwitch,
		AppBar,
		AppShell
	} from '@skeletonlabs/skeleton';
	import logo from '$lib/Images/header-logo-2.png';

	initializeStores();
	const drawerStore = getDrawerStore();

	function drawerOpen(): void {
		drawerStore.open({});
	}
</script>

<div class="grid grid-rows-[auto_1fr_auto]">
	<!-- Header -->
	<header
		class="sticky top-0 z-10 h-12 flex items-center justify-between w-full px-4 dark:bg-surface-700 bg-primary-400"
	>
		<!-- Left-aligned button -->
		<div class="flex justify-start">
			<button class="md:hidden btn btn-sm mr-4" on:click={drawerOpen}>
				<span>
					<svg viewBox="0 0 100 80" class="fill-token w-4 h-4">
						<rect width="100" height="20" />
						<rect y="30" width="100" height="20" />
						<rect y="60" width="100" height="20" />
					</svg>
				</span>
			</button>
		</div>

		<!-- Centered logo -->
		<div class="flex justify-center flex-grow">
			<img alt="The project logo" src={logo} />
		</div>

		<!-- Right-aligned light switch -->
		<div class="flex justify-end">
			<LightSwitch />
		</div>
	</header>

	<!-- Grid Columns -->
	<div class="grid grid-cols-1 md:grid-cols-[auto_1fr]">
		<!-- Left Sidebar. -->
		<aside class="hidden md:block dark:bg-surface-700 bg-primary-400 sticky top-12 h-screen">
			<Navigation />
		</aside>
		<!-- Main Content -->
		<main>
			<slot />
		</main>
	</div>

	<!-- Footer -->
	<footer class="footer p-6 bg-surface bg-surface-200-700-token">
		<div class="container mx-auto text-center space-y-4">
			<p class="text-lg font-semibold">© 2024 Your Company Name</p>
			<p class="text-sm">All rights reserved.</p>
			<div class="space-x-4">
				<a href="/privacy-policy">Privacy Policy</a>
				<a href="/terms-of-service">Terms of Service</a>
			</div>
		</div>
	</footer>
</div>

<!-- Mobile Sidebar: This hides when the screen grows larger than md because of "md:hidden"-->
<Drawer>
	<Navigation />
</Drawer>

<style>
	/* Make the image responsive */
	img {
		width: 140px; /* Image scales with the width of its container */
		height: auto; /* Maintain the aspect ratio */
		display: block; /* Removes extra space below the image */
		margin: 0 auto; /* Center the image horizontally */
	}

	main {
		background-image: radial-gradient(
				at 0% 0%,
				rgba(var(--color-surface-500) / 0.33) 0px,
				transparent 50%
			),
			radial-gradient(at 98% 1%, rgba(var(--color-primary-500) / 0.33) 0px, transparent 50%);
		background-attachment: fixed;
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
	}

	header {
		background-image: radial-gradient(
				at 0% 0%,
				rgba(var(--color-surface-500) / 0.33) 0px,
				transparent 50%
			),
			radial-gradient(at 98% 0%, rgba(var(--color-secondary-500) / 0.33) 0px, transparent 50%);
		background-attachment: fixed;
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
	}

	aside {
		background-image: radial-gradient(
				at 0% 0%,
				rgba(var(--color-surface-500) / 0.33) 0px,
				transparent 50%
			),
			radial-gradient(at 0% 98%, rgba(var(--color-secondary-500) / 0.33) 0px, transparent 50%);
		background-attachment: fixed;
		background-position: center;
		background-repeat: no-repeat;
		background-size: cover;
	}
</style>
