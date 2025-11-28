<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import ProjectModal from '$lib/components/common/ProjectModal.svelte';
	import ShowcaseCard from './ShowcaseCard.svelte';
	import ImageModal from '$lib/components/common/ImageModal.svelte';

	gsap.registerPlugin(ScrollTrigger);

	let isModalOpen = false;
	let selectedProject: any = null;

	let isImageModalOpen = false;
	let selectedImageSrc = '';
	let selectedImageAlt = '';

	let selectedImages: string[] = [];

	onMount(() => {
		// Wait for DOM to be fully ready before initializing animations
		setTimeout(() => {
			// GSAP ScrollTrigger animations with optimized performance
			// Section header animation
			gsap.fromTo(
				'.home-showcases h2',
				{ opacity: 0, y: 30 },
				{
					opacity: 1,
					y: 0,
					duration: 0.6,
					ease: 'power2.out',
					scrollTrigger: {
						trigger: '.home-showcases',
						start: 'top 90%',
						end: 'top 30%',
						toggleActions: 'play none play reverse'
					}
				}
			);

			// Client apps grid animation
			gsap.fromTo(
				'.home-showcases .grid.grid-cols-1 .group.relative',
				{ opacity: 0, scale: 0.9, y: 30 },
				{
					opacity: 1,
					scale: 1,
					y: 0,
					duration: 0.7,
					ease: 'back.out(1.5)',
					stagger: 0.08,
					scrollTrigger: {
						trigger: '.home-showcases .grid.grid-cols-1',
						start: 'top 85%',
						end: 'top 30%',
						toggleActions: 'play none play reverse'
					}
				}
			);

			// Immersive Zoom Animation
			gsap.fromTo(
				'.immersive-text',
				{
					scale: 800,
					opacity: 1,
					color: '#000000', // Start with black text (invisible on black background)
					transformOrigin: '10% 50%' // Targeting solid black area in 'M' or 'i' of Minhas
				},
				{
					scale: 1,
					opacity: 1,
					color: '#000000', // End with black text
					ease: 'power2.out',
					scrollTrigger: {
						trigger: '.immersive-wrapper',
						start: 'top top',
						end: 'bottom bottom',
						scrub: 1
					}
				}
			);

			// Animate background from black to white as text zooms out
			gsap.fromTo(
				'.immersive-container',
				{
					backgroundColor: '#000000' // Start with black background
				},
				{
					backgroundColor: '#ffffff', // End with white background
					ease: 'power2.out',
					scrollTrigger: {
						trigger: '.immersive-wrapper',
						start: 'top top',
						end: 'bottom bottom',
						scrub: 1
					}
				}
			);
		}, 50); // Small delay to ensure DOM is ready
	});

	function openProjectModal(project: any) {
		selectedProject = project;
		isModalOpen = true;
	}

	function openImageModal(src: string, alt: string, images: string[] = []) {
		selectedImageSrc = src;
		selectedImageAlt = alt;
		selectedImages = images;
		isImageModalOpen = true;
	}

	import { toolIcons, getToolIcon } from '$lib/config/toolIcons';

	const clientApps = [
		{
			id: '1',
			name: 'acannabis.legal: Plataforma de Cannabis Medicinal',
			image: '/assets/img/clients/acannabis.gif',
			link: 'https://acannabis.legal/',
			description:
				'Plataforma web completa para o mercado legal de cannabis, oferecendo informações regulatórias, produtos certificados e conexão entre usuários e fornecedores autorizados.',
			role: 'Arquiteto de Software & Full Stack Developer',
			year: '2023',
			technologies: ['Angular', 'TailwindCSS', 'ThreeJS', 'Go', 'WebRTC', 'Stripe'],
			features: [
				'Sistema de autenticação e autorização multi-nível',
				'Catálogo de produtos com filtros avançados',
				'Painel administrativo para gerenciamento de conteúdo',
				'Integração com APIs de pagamento',
				'Sistema de notificações em tempo real'
			],
			stackImages: ['Angular', 'Go', 'WebRTC', 'Stripe'].map((t) => getToolIcon(t) ?? ''),
			stackImageNames: ['Angular', 'Go', 'WebRTC', 'Stripe'],
			backgroundColor: '#4CAF50',
			type: 'desktop',
			phoneImages: [
				'/assets/img/clients/cannabislegal-logo.png',
				'/assets/img/clients/acannabis.jpg'
			]
		},
		{
			id: '2',
			name: 'EduCanoas: App de gestão educacional',
			image: '/assets/img/clients/educanoas.gif',
			link: 'https://apkpure.com/br/educanoas/br.com.abaco.rs.canoas.educanoas',
			description:
				'Aplicativo mobile de gestão educacional para escolas, permitindo acompanhamento de alunos, comunicação com pais, gerenciamento de notas, frequência e atividades escolares.',
			role: 'Lead Mobile Developer',
			year: '2022-2023',
			technologies: ['Ionic', 'Android', 'iOS', 'Cordova', 'Firebase'],
			features: [
				'Painel para professores, alunos e pais',
				'Sistema de mensagens e notificações push',
				'Controle de frequência e notas',
				'Calendário de eventos e atividades',
				'Compartilhamento de documentos e materiais',
				'Sincronização offline'
			],
			stackImages: ['Ionic', 'Android', 'iOS', 'Cordova'].map((t) => getToolIcon(t) ?? ''),
			stackImageNames: ['Ionic', 'Android', 'iOS', 'Cordova'],
			backgroundColor: '#FFFFFF',
			titleColor: '#2196F3',
			type: 'mobile',
			phoneImages: ['/assets/img/clients/educanoas1.png', '/assets/img/clients/educanoas2.png']
		},
		{
			id: '3',
			name: 'Skill: Landing Page + Gerenciamento de LAN',
			image: '/assets/img/clients/skill.gif',
			link: 'https://skill.unrender.dev/',
			description:
				'Interface web moderna para sistema de gerenciamento de rede local (LAN), oferecendo controle de dispositivos, monitoramento de tráfego e configuração de rede de forma intuitiva.',
			role: 'Frontend Architect',
			year: '2023',
			technologies: ['Svelte', 'TailwindCSS', 'Go', 'Qt'],
			features: [
				'Dashboard em tempo real com métricas de rede',
				'Visualização de dispositivos conectados',
				'Controle de largura de banda',
				'Sistema de alertas e logs',
				'Interface responsiva e moderna',
				'Temas claro e escuro'
			],
			stackImages: ['Svelte', 'TailwindCSS', 'Go', 'Qt'].map((t) => getToolIcon(t) ?? ''),
			stackImageNames: ['Svelte', 'TailwindCSS', 'Go', 'Qt'],
			backgroundColor: '#ef4444',
			type: 'desktop-left',
			phoneImages: ['/assets/img/clients/skilllan1.jpg', '/assets/img/clients/skilllan2.png']
		}
	];

	const myApps = [
		{
			id: 1,
			name: 'ng-tropicaliacraft-landingpage',
			image: '/assets/img/apps/tropicalia.webp',
			link: 'https://play.google.com/store/apps/details?id=io.sensify.sensor',
			caption:
				'Landing Page para o TropicaliaCraft em Angular (SSG) com hidratação zoneless + Serviços em Go/Fiber',
			background: '#E1E1E1',
			demoUrl: 'https://tropicaliacraft.online/',
			githubUrl: 'https://github.com/gustavodslara/ng-tropicaliacraft-landing-page'
		},
		{
			id: 2,
			name: 'svelte-threejs-tech-store',
			image: '/assets/img/apps/techstore.webp',
			link: 'https://play.google.com/store/apps/details?id=com.taru',
			caption: 'Landing Page em SvelteKit e TailwindCSS + Animações com GSAP e Three.js',
			background: '#F5E7B4',
			demoUrl: 'https://techstore.gustavodslara.pro/',
			githubUrl: 'https://github.com/gustavodslara/svelte-threejs-tech-store'
		},
		{
			id: 3,
			name: 'Servidores do TropicaliaCraft e Serviços em Go/Fiber',
			image: '/assets/img/apps/server.webp',
			link: 'https://play.google.com/store/apps/details?id=com.hundi.social',
			caption:
				'Gestão da Infraestrutura dos servidores + Versionamento do Fabric, Paper e mods/plugins, e deploy automatizado com GitHub Actions na Azure',
			background: '#3CE79F',
			full: true,
			demoUrl: 'https://ecraft.tropicaliacraft.online/?server=crossplay.tropicaliacraft.online',
			githubUrl: 'https://github.com/organizations/tropicaliacraft/repositories/'
		}
	];

	// GitHub Repo Name Mapping (DePara/FromTo)
	// Map static images to GitHub repository names
	const repoMapping: Record<string, string> = {
		phanteon: 'phanteon-launcher',
		voxelcanvas: 'voxel-canvas',
		worldtrip: 'world-trip-app',
		tropicalialauncher: 'tropicalialauncher',
		polyui: 'polyui',
		argusplayer: 'argusplayer',
		tourvirtual: 'svelte-threejs-tour-virtual'
	};

	// Static logos (will be replaced with GitHub API data)
	// TODO: Fetch from GitHub API - https://api.github.com/users/gustavodslara/repos
	const logos = [
		{
			src: '/assets/img/logos/phanteon.png',
			name: 'Pantheon Launcher',
			color: '#e57373',
			repoName: repoMapping['phanteon'],
			description: 'Landing Page em Svelte',
			githubUrl: 'https://github.com/gustavodslara/pantheon-launcher',
			demoUrl: 'https://pantheon.gustavodslara.pro/'
		},
		{
			src: '/assets/img/logos/voxelcanvas.png',
			name: 'Voxel Canvas',
			color: '#81c784',
			repoName: repoMapping['voxelcanvas'],
			description: 'Paint 3D cúbico',
			githubUrl: 'https://github.com/gustavodslara/threejs-voxel-canvas',
			demoUrl: 'https://voxelcanvas.gustavodslara.pro/'
		},
		{
			src: '/assets/img/logos/worldtrip.png',
			name: 'World Trips Album',
			color: '#ffb74d',
			repoName: repoMapping['worldtrip'],
			description: 'Album interativo de viagens em 3D',
			githubUrl: 'https://github.com/gustavodslara/ng-threejs-world-trips',
			demoUrl: 'https://trips.gustavodslara.pro/'
		},
		{
			src: '/assets/img/logos/tropicalialauncher.png',
			name: 'Tropicalia Launcher',
			color: '#e57373',
			repoName: repoMapping['tropicalialauncher'],
			description: 'Fork do PrismLauncher',
			githubUrl: 'https://github.com/gustavodslara/PrismLauncher/',
			demoUrl: 'https://tropicaliacraft.online/'
		},
		{
			src: '/assets/img/logos/polyui.png',
			name: 'PolyUI',
			color: '#ffb74d',
			repoName: repoMapping['polyui'],
			description: 'Interface Web para IA local',
			githubUrl: 'https://github.com/gustavodslara/poly-ui',
			demoUrl: 'https://polyui.gustavodslara.pro/'
		},
		{
			src: '/assets/img/logos/argusplayer.png',
			name: 'Argus Player',
			color: '#64b5f6',
			repoName: repoMapping['argusplayer'],
			description: 'Streaming de mídia local',
			githubUrl: 'https://github.com/gustavodslara/argus-player',
			demoUrl: 'https://argus.gustavodslara.pro/'
		},
		{
			src: '/assets/img/logos/virtualtour.png',
			name: 'WebXR Tour Virtual',
			color: '#81c784',
			repoName: repoMapping['tourvirtual'],
			description: 'Tour em realidade virtual',
			githubUrl: 'https://github.com/gustavodslara/svelte-threejs-tour-virtual',
			demoUrl: 'https://tourvirtual.gustavodslara.pro/'
		}
	];
</script>

<div id="showcases" class="home-showcases py-8 md:py-16 px-4 md:px-8 lg:px-12">
	<!-- Client Projects Section (Closed Source) -->
	<div class="mb-0 md:mb-0">
		<h2 class="text-3xl md:text-4xl font-medium whitespace-nowrap">Projetos de Clientes</h2>
	</div>

	<div class="max-w-7xl mx-auto">
		<div class="h-12 md:h-16"></div>

		<div class="mb-12 md:mb-16">
			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 md:gap-8">
				{#each clientApps as app, i}
					<div class="showcase-card-wrapper h-full" style="animation-delay: {i * 0.1}s;">
						<ShowcaseCard
							name={app.name}
							description={app.description}
							stackImages={app.stackImages}
							stackImageNames={app.stackImageNames ?? []}
							backgroundColor={app.backgroundColor}
							titleColor={app.titleColor || '#ffffff'}
							phoneImages={app.phoneImages}
							type={app.type === 'desktop'
								? 'desktop'
								: app.type === 'desktop-left'
									? 'desktop-left'
									: 'mobile'}
							onImageClick={(src) => openImageModal(src, app.name, app.phoneImages)}
						/>
					</div>
				{/each}
			</div>
		</div>

		<div class="h-12 md:h-16"></div>
	</div>

	<!-- Personal Projects Section (Open Source - GitHub) -->
	<div class="mb-6 md:mb-9">
		<h2 class="text-3xl md:text-4xl font-medium whitespace-nowrap">Projetos Pessoais</h2>
	</div>

	<div class="max-w-7xl mx-auto">
		<div class="mb-12 md:mb-16">
			<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
				{#each myApps as app, i}
					<div
						class="group relative rounded-xl p-6 md:p-8 text-black transition-all duration-300 flex flex-col md:flex-row items-center justify-between gap-4 hover:-translate-y-2 hover:shadow-xl overflow-hidden cursor-pointer"
						class:col-span-full={app.full}
						style="background: {app.background}; animation-delay: {i * 0.1}s;"
					>
						<!-- Open Source Ribbon -->
						<div class="absolute top-0 right-0 z-10 w-[150px] h-[150px] overflow-hidden">
							<span
								class="block absolute w-[200px] py-2 bg-green-500 text-white text-center text-xs font-medium rotate-45 top-[30px] -right-[50px] shadow-lg"
							>
								Open Source
							</span>
						</div>

						<div class="flex-1">
							<p class="text-sm text-black/60 mb-2 m-0">{app.caption}</p>
							<h5 class="text-xl md:text-2xl font-semibold m-0">{app.name}</h5>
						</div>
						<div class="flex-shrink-0">
							<img
								src={app.image}
								alt={app.name}
								class="max-w-[120px] md:max-w-[150px] h-auto rounded-lg transition-transform duration-300 group-hover:scale-95"
							/>
						</div>

						<!-- Hover/Tap Overlay with Animation -->
						<div
							class="absolute inset-0 bg-black/90 opacity-0 group-hover:opacity-100 group-active:opacity-100 transition-all duration-300 flex flex-col items-center justify-center p-6 md:p-8 gap-4 transform scale-95 group-hover:scale-100 z-20"
						>
							<h5 class="text-white font-semibold text-lg md:text-xl text-center">{app.name}</h5>
							<p class="text-white/90 text-sm md:text-base text-center line-clamp-2">
								{app.caption}
							</p>
							<div class="flex gap-3 flex-wrap justify-center">
								<a
									href={app.demoUrl}
									target="_blank"
									rel="noopener"
									class="bg-white text-black px-4 py-2 rounded-lg text-sm font-medium hover:bg-gray-200 transition-colors no-underline"
								>
									Ver
								</a>
								<a
									href={app.githubUrl}
									target="_blank"
									rel="noopener"
									class="bg-green-500 text-white px-4 py-2 rounded-lg text-sm font-medium hover:bg-green-600 transition-colors no-underline flex items-center gap-2"
								>
									<svg class="w-4 h-4" fill="currentColor" viewBox="0 0 24 24"
										><path
											d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
										/></svg
									>
									Código
								</a>
							</div>
						</div>
					</div>
				{/each}
			</div>
		</div>
	</div>

	<div class="h-12 md:h-16"></div>

	<!-- More Personal Projects Section (GitHub API - Interactive) -->
	<div class="mb-6 md:mb-14">
		<h2 class="text-3xl md:text-4xl font-medium whitespace-nowrap">Mais Projetos Pessoais</h2>
	</div>

	<div class="max-w-7xl mx-auto">
		<div>
			<div class="flex flex-wrap gap-3">
				{#each logos as logo, i}
					<button
						class="group relative flex-1 min-w-[100px] md:min-w-[120px] p-6 md:p-8 rounded-xl flex items-center justify-center transition-all duration-300 hover:scale-110 hover:z-10 overflow-hidden"
						style="background: {logo.color}; animation-delay: {0.3 + i * 0.05}s;"
						on:click={() => {}}
					>
						<!-- Open Source Ribbon -->
						<div class="absolute top-0 right-0 z-10 w-[100px] h-[100px] overflow-hidden">
							<span
								class="block absolute w-[140px] py-1 bg-green-500 text-white text-center text-[10px] font-medium rotate-45 top-[20px] -right-[35px] shadow-lg"
							>
								Open Source
							</span>
						</div>

						<img
							src={logo.src}
							alt={logo.name}
							class="max-w-full h-auto transition-transform duration-300 group-hover:scale-90"
						/>

						<!-- Hover/Tap Overlay with Animation -->
						<div
							class="absolute inset-0 bg-black/90 opacity-0 group-hover:opacity-100 group-active:opacity-100 transition-all duration-300 flex flex-col items-center justify-center p-4 gap-3 transform scale-95 group-hover:scale-100"
						>
							<h5 class="text-white font-semibold text-sm md:text-base text-center">{logo.name}</h5>
							<p class="text-white/80 text-xs md:text-sm text-center line-clamp-2">
								{logo.description}
							</p>
							<div class="flex gap-2">
								<a
									href={logo.demoUrl}
									target="_blank"
									rel="noopener"
									class="bg-white text-black px-3 py-1.5 rounded text-xs font-medium hover:bg-gray-200 transition-colors no-underline"
								>
									Ver
								</a>
								<a
									href={logo.githubUrl}
									target="_blank"
									rel="noopener"
									class="bg-green-500 text-white px-3 py-1.5 rounded text-xs font-medium hover:bg-green-600 transition-colors no-underline flex items-center gap-1"
								>
									<svg class="w-3 h-3" fill="currentColor" viewBox="0 0 24 24"
										><path
											d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"
										/></svg
									>
									Código
								</a>
							</div>
						</div>
					</button>
				{/each}
			</div>
		</div>
	</div>
</div>

<!-- Immersive Zoom Section for "Minhas Plataformas" -->
<div class="immersive-wrapper relative h-[200vh]">
	<div id="platforms" class="absolute w-full h-px pointer-events-none" style="top: 180vh;"></div>
	<div
		class="immersive-container sticky top-0 h-screen flex items-end justify-start overflow-hidden bg-black pb-16 md:pb-24 px-4 md:px-8 lg:px-12"
		style="z-index: 1;"
	>
		<h2
			class="immersive-text text-3xl md:text-4xl font-medium text-left whitespace-nowrap text-black"
		>
			Minhas Plataformas
		</h2>
	</div>
</div>

<!-- Project Modal -->
{#if selectedProject}
	<ProjectModal bind:isOpen={isModalOpen} project={selectedProject} />
{/if}

<!-- Image Modal -->
<ImageModal
	bind:isOpen={isImageModalOpen}
	imageSrc={selectedImageSrc}
	altText={selectedImageAlt}
	images={selectedImages}
/>

<style>
	/* GSAP handles animations */
</style>
