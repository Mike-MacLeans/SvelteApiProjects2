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

<div class="grid grid-rows-[auto_1fr_auto] bg-surface-200-700-token">
	<!-- Header -->
	<header class="sticky top-0 z-10 h-16">
		<AppBar
			gridColumns="grid-cols-3"
			slotDefault="place-self-center"
			slotTrail="place-content-end"
			background="bg-surface-200-700-token"
		>
			<svelte:fragment slot="lead">
				<div class="flex items-center justify-center">
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
			</svelte:fragment>
			<img alt="The project logo" src={logo} />
			<svelte:fragment slot="trail">
				<LightSwitch />
			</svelte:fragment>
		</AppBar>
	</header>

	<!-- Grid Columns -->
	<div class="grid grid-cols-1 md:grid-cols-[auto_1fr]">
		<!-- Left Sidebar. -->
		<aside class="hidden md:block bg-surface-100-800-token sticky top-16 h-screen">
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

<!--Mobile Sidebar: This hides when the screen grows larger than md because of "md:hidden"-->
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
</style>
