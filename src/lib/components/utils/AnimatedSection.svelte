<script lang="ts">
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';

	let visible = false;
	let element: HTMLElement;

	onMount(() => {
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting && !visible) {
					visible = true;
				}
			},
			{
				threshold: 0.1,
				rootMargin: '50px'
			}
		);

		if (element) {
			observer.observe(element);
		}

		return () => {
			if (element) {
				observer.unobserve(element);
			}
		};
	});
</script>

<div bind:this={element} class="animated-section">
	<slot />
</div>

<style>
	.animated-section {
		width: 100%;
	}
</style>

