<script lang="ts">
	import { getDrawerStore } from '@skeletonlabs/skeleton';
	import { fade, fly } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	const drawerStore = getDrawerStore();

	function drawerClose(): void {
		drawerStore.close();
	}

	interface SlidefadeParams {
		delay?: number;
		duration?: number;
		easing?: (t: number) => number;
	}

	export function slidefade(node: HTMLElement, params: SlidefadeParams) {
		// Get the existing transform property of the node
		const existingTransform = getComputedStyle(node).transform.replace('none', '');

		return {
			delay: params.delay || 0,
			duration: params.duration || 500,
			easing: params.easing || cubicOut,
			css: (t: number, u: number) =>
				`transform-origin: top left; transform: ${existingTransform} scaleY(${t}); opacity: ${t};`
		};
	}
</script>

<nav class="list-nav p-4 md:bg-custom-gradient">
	<ul>
		<li>
			<a href="/" on:click={drawerClose} transition:slidefade={{ delay: 0 }}>Homepage</a>
		</li>
		<li>
			<a href="/about" on:click={drawerClose} transition:slidefade={{ delay: 75 }}>About</a>
		</li>
		<li>
			<a href="/blog" on:click={drawerClose} transition:slidefade={{ delay: 150 }}>Blog</a>
		</li>
		<li>
			<a href="/contact" on:click={drawerClose} transition:slidefade={{ delay: 225 }}>Contact</a>
		</li>
	</ul>
</nav>

<style>
	/* Remove gradient or apply different background for md screens and above */
	@media (max-width: 768px) {
		nav {
			background-image: radial-gradient(
					at 0% 0%,
					rgba(var(--color-error-500) / 0.33) 0px,
					transparent 50%
				),
				radial-gradient(at 98% 1%, rgba(var(--color-error-500) / 0.33) 0px, transparent 50%);
			background-attachment: fixed;
			background-position: center;
			background-repeat: no-repeat;
			background-size: cover;
		}
	}
</style>
