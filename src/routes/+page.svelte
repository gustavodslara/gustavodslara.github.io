<script lang="ts">
	import Navbar from '$lib/components/layout/Navbar.svelte';
	import HomeTop from '$lib/components/home/HomeTop.svelte';
	import HomeAbout from '$lib/components/home/HomeAbout.svelte';
	import HomeEducation from '$lib/components/home/HomeEducation.svelte';
	import HomeShowcases from '$lib/components/home/HomeShowcases.svelte';
	import HomePlatforms from '$lib/components/home/HomePlatforms.svelte';
	import HomeContact from '$lib/components/home/HomeContact.svelte';
	import Footer from '$lib/components/common/Footer.svelte';
</script>

<svelte:head>
	<title>Gustavo Lara | Software Architect</title>
	<meta
		name="description"
		content="Portfolio of Gustavo Lara - Software Architect from Brasil, specialized in microservices, scalable distributed systems, and fullstack development (Angular, Svelte, Flutter, Android, iOS)."
	/>
</svelte:head>

<Navbar />

<main class="flex-1 w-full">
	<!-- Navbar spacer -->
	<div class="h-20 md:h-24"></div>

	<HomeTop />

	<div class="h-12 md:h-16"></div>
	<HomeAbout />

	<div class="h-12 md:h-20"></div>
	<HomeEducation />

	<div class="h-12 md:h-20"></div>
	<HomeShowcases />

	<HomePlatforms />

	<div class="h-12 md:h-20"></div>
	<HomeContact />

	<div class="h-12 md:h-16"></div>
	<Footer />
</main>
