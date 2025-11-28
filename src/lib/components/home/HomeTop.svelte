<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	
	gsap.registerPlugin(ScrollTrigger);
	
	let mounted = false;
	let h4Element: HTMLElement;
	let h2_1: HTMLElement;
	let h2_2: HTMLElement;
	let h2_3: HTMLElement;
	let pElement: HTMLElement;
	let imageContainer: HTMLElement;
	
	onMount(() => {
		mounted = true;
		
		// Wait for DOM to be fully ready before initializing animations
		setTimeout(() => {
			if (h4Element && h2_1 && h2_2 && h2_3 && pElement && imageContainer) {
		// Create a timeline with ScrollTrigger for scroll-attached animations
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: h4Element,
				start: "top 90%",
				end: "bottom 30%",
				toggleActions: "play none play reverse"
			}
		});
		
		// Animate h4
		tl.fromTo(h4Element, 
			{ opacity: 0, y: 30 }, 
			{ opacity: 1, y: 0, duration: 0.6, ease: "power2.out" }
		);
		
		// Animate h2 elements with stagger
		tl.fromTo([h2_1, h2_2, h2_3], 
			{ opacity: 0, y: 40, rotationX: -10 }, 
			{ 
				opacity: 1, 
				y: 0, 
				rotationX: 0, 
				duration: 0.9, 
				ease: "back.out(1.4)", 
				stagger: 0.15 
			}, 
			"-=0.4"
		);
		
		// Animate paragraph
		tl.fromTo(pElement, 
			{ opacity: 0, y: 20 }, 
			{ opacity: 1, y: 0, duration: 0.5, ease: "power2.out" }, 
			"-=0.3"
		);
		
		// Animate image with scale and glow effect
		tl.fromTo(imageContainer, 
			{ opacity: 0, scale: 0.9, rotationY: 10 }, 
			{ 
				opacity: 1, 
				scale: 1, 
				rotationY: 0, 
				duration: 1, 
				ease: "elastic.out(1, 0.4)" 
			}, 
			"-=0.7"
		);				// Add continuous subtle animation to the image
				gsap.to(imageContainer, {
					y: -8,
					duration: 2.5,
					ease: "power2.inOut",
					yoyo: true,
					repeat: -1,
					delay: 1.5
				});
			}
		}, 50); // Reduced delay and optimized for better performance
	});
</script>

<div id="home" class="min-h-[70vh] flex items-center px-4 md:px-8 lg:px-12">
	<div class="max-w-7xl mx-auto w-full">
		<div class="h-16 md:h-32"></div>

		<div class="grid grid-cols-1 lg:grid-cols-2 gap-8 lg:gap-12 items-center">
			<!-- Left Content -->
			<div>
				{#if mounted}
					<h4 bind:this={h4Element} class="text-xl md:text-2xl font-normal text-black mb-4 md:mb-6">
						Olá, eu sou Gustavo Lara
					</h4>

					<h2 bind:this={h2_1} class="text-4xl md:text-6xl lg:text-7xl font-extralight leading-tight text-black mb-1" style="font-family: 'Clash Display', sans-serif;">
						Arquiteto
					</h2>
					<h2 bind:this={h2_2} class="text-4xl md:text-6xl lg:text-7xl font-extralight leading-tight text-black mb-1" style="font-family: 'Clash Display', sans-serif;">
						de Software
					</h2>
					<h2 bind:this={h2_3} class="text-4xl md:text-6xl lg:text-7xl font-extralight leading-tight text-black mb-6 md:mb-8" style="font-family: 'Clash Display', sans-serif;">
						& Líder Técnico
					</h2>

					<p bind:this={pElement} class="text-base md:text-lg leading-relaxed text-black/70 max-w-2xl">
						Arquiteto de Software com vasta experiência em modernização de legado, arquiteturas distribuídas e interoperabilidade com código nativo. 
					</p>
					<p bind:this={pElement} class="text-base md:text-lg leading-relaxed text-black/70 max-w-2xl">
						Perfil poliglota, com alta adaptabilidade a novas linguagens e ecossistemas.
					</p>
				{/if}
			</div>

			<!-- Right Profile Picture -->
			{#if mounted}
				<div bind:this={imageContainer} class="flex items-center justify-center lg:justify-end">
					<div class="relative w-full max-w-md lg:max-w-lg">
						<div class="absolute inset-0 bg-gradient-to-br from-[#dd206b]/20 to-[#667eea]/20 rounded-full blur-3xl transform scale-110"></div>
						<img 
							src="/assets/img/avatar/pic_avatar.png" 
							alt="Gustavo Lara" 
							class="relative w-full h-auto rounded-2xl shadow-2xl transform hover:scale-105 transition-transform duration-500"
						/>
					</div>
				</div>
			{/if}
		</div>

		<div class="h-16 md:h-32"></div>
	</div>
</div>

<style>
	/* No custom styles needed, using GSAP for animations */
</style>
