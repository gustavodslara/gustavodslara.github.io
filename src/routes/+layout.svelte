<script lang="ts">
	import '../app.scss';
</script>

<div class="app">
	<slot />
</div>

<style lang="scss">
	:global(html) {
		scroll-behavior: smooth !important;
		scroll-padding-top: 120px !important;
	}

	:global(body) {
		margin: 0;
		padding: 0;
		scroll-behavior: smooth !important;
	}

	:global(*) {
		scroll-behavior: smooth !important;
	}

	.app {
		display: flex;
		flex-direction: column;
		min-height: 100vh;
	}
</style>
