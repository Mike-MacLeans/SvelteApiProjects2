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

<!-- App Shell -->
<Drawer>
	<Navigation />
</Drawer>
<AppShell slotSidebarLeft="bg-surface-500/5 w-0 lg:w-64">
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar gridColumns="grid-cols-3" slotDefault="place-self-center" slotTrail="place-content-end">
			<svelte:fragment slot="lead">
				<div class="flex items-center justify-center">
					<button class="lg:hidden btn btn-sm mr-4" on:click={drawerOpen}>
						<span>
							<svg viewBox="0 0 100 80" class="fill-token w-4 h-4">
								<rect width="100" height="20" />
								<rect y="30" width="100" height="20" />
								<rect y="60" width="100" height="20" />
							</svg>
						</span>
					</button>
					<img alt="The project logo" src={logo} />
				</div>
			</svelte:fragment>

			<svelte:fragment slot="trail">
				<LightSwitch />
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>

	<svelte:fragment slot="sidebarLeft">
		<Navigation />
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>

<style>
	/* Make the image responsive */
	img {
		width: 140px; /* Image scales with the width of its container */
		height: auto; /* Maintain the aspect ratio */
		display: block; /* Removes extra space below the image */
		margin: 0 auto; /* Center the image horizontally */
	}
</style>
