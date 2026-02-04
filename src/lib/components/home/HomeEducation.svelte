<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let openEducation: Set<number> = new Set();
	let isMobile = false;

	onMount(() => {
		// Check if mobile
		isMobile = window.innerWidth < 768;

		// Open education items based on device
		if (isMobile) {
			// On mobile, only first item is open
			openEducation = new Set([1]);
		} else {
			// On desktop, open all items
			openEducation = new Set([1, 2, 3]);
		}

		// Wait for DOM to be fully ready before initializing animations
		setTimeout(() => {
			// GSAP ScrollTrigger animations with optimized performance
			// Section header animation
			gsap.fromTo(
				'.home-education .flex.items-end.gap-3.mb-6',
				{ opacity: 0, y: 30 },
				{
					opacity: 1,
					y: 0,
					duration: 0.6,
					ease: 'power2.out',
					scrollTrigger: {
						trigger: '.home-education',
						start: 'top 90%',
						end: 'top 30%',
						toggleActions: 'play none play reverse'
					}
				}
			);

			// Education timeline animation
			gsap.fromTo(
				'.home-education .relative.pl-4 .relative.mb-6',
				{ opacity: 0, x: -30 },
				{
					opacity: 1,
					x: 0,
					duration: 0.6,
					ease: 'power2.out',
					stagger: 0.15,
					scrollTrigger: {
						trigger: '.home-education .relative.pl-4',
						start: 'top 85%',
						end: 'top 35%',
						toggleActions: 'play none play reverse'
					}
				}
			);
		}, 50); // Small delay to ensure DOM is ready
	});

	interface EducationItem {
		id: number;
		institution: string;
		logo: string;
		degree: string;
		field: string;
		startDate: string;
		endDate: string;
		color: string;
		description: string | string[];
		status?: 'completed' | 'in-progress';
	}

	const educationItems: EducationItem[] = [
		{
			id: 1,
			institution: 'Instituto Federal de Mato Grosso',
			logo: '/assets/img/logos/ifmt_logo.png',
			degree: 'Tecnólogo',
			field: 'Sistemas para Internet',
			startDate: '2018',
			endDate: '2021',
			color: '#027DFD',
			description: [
				'Curso Superior de Tecnologia em Sistemas para Internet com foco em desenvolvimento web, programação, banco de dados e arquitetura de aplicações.',
			],
			status: 'completed'
		},
		{
			id: 2,
			institution: 'Anhanguera',
			logo: '/assets/img/logos/anhanguera.png',
			degree: 'MBA',
			field: 'Engenharia de automação e IoT',
			startDate: '2023',
			endDate: '2023',
			color: '#FF6B35',
			description: [
				'MBA em Engenharia de Automação e IoT, focado em tecnologias de automação industrial, Internet das Coisas (IoT), sistemas embarcados e integração de processos industriais.',
			],
			status: 'completed'
		},
		{
			id: 3,
			institution: 'Anhanguera',
			logo: '/assets/img/logos/anhanguera.png',
			degree: 'MBA',
			field: 'Gestão da Tecnologia de Informação',
			startDate: '2025',
			endDate: '2025',
			color: '#4CAF50',
			description: [
				'MBA em Gestão da Tecnologia da Informação, abrangendo estratégias de TI, gestão de projetos tecnológicos, governança de TI e liderança em ambientes digitais.',
			],
			status: 'completed'
		}
	];

	function toggleEducation(id: number) {
		if (openEducation.has(id)) {
			openEducation.delete(id);
		} else {
			openEducation.add(id);
		}
		openEducation = openEducation; // Trigger reactivity
	}
</script>

<div id="education" class="home-education pt-8 md:pt-16 px-4 md:px-8 lg:px-12 bg-white">
	<!-- Section Header -->
	<div class="mb-6 md:mb-8">
		<h2 class="text-3xl md:text-4xl font-medium whitespace-nowrap">Educação</h2>
	</div>

	<div class="max-w-7xl mx-auto pt-4">
		<!-- Education Timeline -->
		<div class="relative pl-4 md:pl-8">
			<!-- Vertical Line -->
			<div class="absolute left-6 top-0 bottom-0 w-0.5 bg-[#027DFD]"></div>

			<!-- Education Items -->
			{#each educationItems as edu, i}
				<div
					class="relative pl-16 cursor-pointer group mb-8"
					style="animation-delay: {0.3 + i * 0.1}s;"
					on:click={() => toggleEducation(edu.id)}
					on:keydown={(e) => e.key === 'Enter' && toggleEducation(edu.id)}
					role="button"
					tabindex="0"
				>
					<!-- Branch Line -->
					<div
						class="absolute left-6 top-4 w-10 h-0.5 transition-all duration-300 group-hover:w-12"
						style="background: {edu.color};"
					></div>

					<!-- Node Circle -->
					<div
						class="absolute left-4 top-2 w-5 h-5 rounded-full border-2 flex items-center justify-center transition-all duration-300 transform group-hover:scale-125 shadow-lg"
						style="background: {openEducation.has(edu.id)
							? edu.color
							: '#fff'}; border-color: {edu.color};"
						class:ring-4={openEducation.has(edu.id)}
						class:ring-opacity-30={openEducation.has(edu.id)}
						style:--tw-ring-color={edu.color}
					>
						{#if openEducation.has(edu.id)}
							<div class="w-2 h-2 rounded-full bg-white"></div>
						{/if}
					</div>

					<!-- Institution Logo Badge -->
					<div
						class="absolute left-0 top-0 w-12 h-12 rounded-full flex items-center justify-center transition-all duration-300 transform group-hover:scale-110 shadow-md overflow-hidden bg-white"
					>
						<img
							src={edu.logo}
							alt="{edu.institution} logo"
							class="w-full h-full object-contain p-1"
						/>
					</div>

					<!-- Education Info Card -->
					<div
						class="bg-white rounded-xl p-4 shadow-md border-2 transition-all duration-300 group-hover:shadow-xl group-hover:-translate-y-1"
						style="border-color: {openEducation.has(edu.id) ? edu.color : 'rgba(0,0,0,0.08)'};"
					>
						<div class="flex items-start justify-between mb-2">
							<div class="flex-1">
								<div class="flex items-center gap-2 flex-wrap">
									<h4 class="text-base md:text-lg font-medium text-black">{edu.degree}</h4>
									{#if edu.status === 'in-progress'}
										<span
											class="text-xs px-2 py-0.5 rounded-full font-medium text-white"
											style="background: {edu.color};"
										>
											Em andamento
										</span>
									{/if}
								</div>
								<p class="text-sm md:text-base text-black/70 font-medium">{edu.field}</p>
								<p class="text-sm text-black/60">{edu.institution}</p>
							</div>
							<div
								class="w-6 h-6 rounded-full flex items-center justify-center transition-transform duration-300 flex-shrink-0"
								class:rotate-90={openEducation.has(edu.id)}
								style="background: {edu.color}30;"
							>
								<span style="color: {edu.color};">→</span>
							</div>
						</div>

						<div class="flex items-center gap-2 text-xs md:text-sm text-black/60 mb-2 flex-wrap">
							<span class="bg-black/5 px-2 md:px-3 py-1 rounded-full">{edu.startDate}</span>
							<span>—</span>
							<span class="bg-black/5 px-2 md:px-3 py-1 rounded-full">{edu.endDate}</span>
						</div>

						<!-- Expandable Description -->
						{#if openEducation.has(edu.id)}
							<div
								class="mt-3 pt-3 border-t border-black/10 text-xs md:text-sm text-black/70 animate-slideDown education-description"
							>
								{#if Array.isArray(edu.description)}
									{#each edu.description as paragraph}
										<p class="mb-3 last:mb-0">{paragraph}</p>
									{/each}
								{:else}
									<p>{edu.description}</p>
								{/if}
							</div>
						{/if}
					</div>
				</div>
			{/each}
		</div>
	</div>
</div>

<style>
	@keyframes slideDown {
		from {
			opacity: 0;
			max-height: 0;
		}
		to {
			opacity: 1;
			max-height: 300px;
		}
	}

	.animate-slideDown {
		animation: slideDown 0.3s ease forwards;
	}

	.ring-4 {
		box-shadow: 0 0 0 4px currentColor;
		opacity: 0.3;
	}

	.education-description p {
		text-align: justify;
		text-indent: 2em;
		line-height: 1.6;
	}

	.education-description p:first-child {
		margin-top: 0;
	}
</style>
