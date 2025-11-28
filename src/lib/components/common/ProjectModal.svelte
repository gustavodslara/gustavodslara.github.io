<script lang="ts">
	import { fade, scale } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

	export let isOpen = false;
	export let project: {
		name: string;
		image: string;
		description: string;
		technologies?: string[];
		features?: string[];
		link?: string;
		githubUrl?: string;
		role?: string;
		year?: string;
	};

	import { toolIcons, getToolIcon } from '$lib/config/toolIcons';

	function closeModal() {
		isOpen = false;
	}

	function handleBackdropClick(event: MouseEvent) {
		if (event.target === event.currentTarget) {
			closeModal();
		}
	}

	function handleKeydown(event: KeyboardEvent) {
		if (event.key === 'Escape') {
			closeModal();
		}
	}
</script>

<svelte:window on:keydown={handleKeydown} />

{#if isOpen}
	<!-- Backdrop -->
	<div 
		class="fixed inset-0 bg-black/60 backdrop-blur-sm z-50 flex items-center justify-center p-4"
		on:click={handleBackdropClick}
		on:keydown={handleKeydown}
		role="button"
		tabindex="-1"
		transition:fade={{ duration: 200 }}
	>
		<!-- Modal Content -->
		<!-- svelte-ignore a11y-click-events-have-key-events -->
		<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
		<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
		<div 
			class="bg-white rounded-2xl shadow-2xl max-w-4xl w-full max-h-[90vh] overflow-y-auto"
			transition:scale={{ duration: 300, easing: quintOut, start: 0.9 }}
			on:click|stopPropagation
			on:keydown|stopPropagation
			role="dialog"
			aria-modal="true"
			tabindex="0"
		>
			<!-- Header -->
			<div class="sticky top-0 bg-white border-b border-gray-200 px-6 md:px-8 py-4 md:py-6 flex items-start justify-between z-10 rounded-t-2xl">
				<div class="flex-1 pr-4">
					<h3 class="text-2xl md:text-3xl font-semibold text-gray-900 mb-1">{project.name}</h3>
					{#if project.role || project.year}
						<div class="flex flex-wrap gap-3 text-sm text-gray-600">
							{#if project.role}
								<span class="flex items-center gap-1">
									<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
									</svg>
									{project.role}
								</span>
							{/if}
							{#if project.year}
								<span class="flex items-center gap-1">
									<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
									</svg>
									{project.year}
								</span>
							{/if}
						</div>
					{/if}
				</div>
				<button 
					on:click={closeModal}
					class="flex-shrink-0 w-8 h-8 flex items-center justify-center rounded-full hover:bg-gray-100 transition-colors"
					aria-label="Close modal"
				>
					<svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
						<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
					</svg>
				</button>
			</div>

			<!-- Body -->
			<div class="px-6 md:px-8 py-6 md:py-8">
				<!-- Image -->
				<div class="mb-6 md:mb-8">
					<img 
						src={project.image} 
						alt={project.name}
						class="w-full h-auto rounded-xl shadow-lg object-cover max-h-[400px]"
					/>
				</div>

				<!-- Description -->
				<div class="mb-6 md:mb-8">
					<h4 class="text-lg font-semibold text-gray-900 mb-3">Sobre o Projeto</h4>
					<p class="text-gray-700 leading-relaxed">{project.description}</p>
				</div>

				<!-- Technologies -->
				{#if project.technologies && project.technologies.length > 0}
					<div class="mb-6 md:mb-8">
						<h4 class="text-lg font-semibold text-gray-900 mb-3">Tecnologias</h4>
								<div class="flex flex-wrap gap-2 items-center">
									{#each project.technologies as tech}
										{#if getToolIcon(tech)}
											<div
												class="w-8 h-8 md:w-9 md:h-9 bg-white/20 rounded-full flex items-center justify-center p-1.5 shadow-sm"
												title={tech}
												aria-label={tech}
											>
												<img src={getToolIcon(tech)} alt={tech} class="w-full h-full object-contain" />
											</div>
										{:else}
											<span class="px-3 py-1.5 bg-blue-50 text-blue-700 rounded-lg text-sm font-medium">{tech}</span>
										{/if}
									{/each}
								</div>
					</div>
				{/if}

				<!-- Features -->
				{#if project.features && project.features.length > 0}
					<div class="mb-6 md:mb-8">
						<h4 class="text-lg font-semibold text-gray-900 mb-3">Principais Funcionalidades</h4>
						<ul class="space-y-2">
							{#each project.features as feature}
								<li class="flex items-start gap-2 text-gray-700">
									<svg class="w-5 h-5 text-green-500 flex-shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
										<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
									</svg>
									<span>{feature}</span>
								</li>
							{/each}
						</ul>
					</div>
				{/if}

				<!-- Action Buttons -->
				<div class="flex flex-wrap gap-3 pt-4 border-t border-gray-200">
					{#if project.link}
						<a 
							href={project.link}
							target="_blank"
							rel="noopener noreferrer"
							class="flex-1 min-w-[200px] px-6 py-3 bg-black text-white rounded-lg font-medium text-center hover:bg-gray-800 transition-colors flex items-center justify-center gap-2 no-underline"
						>
							<svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
								<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14" />
							</svg>
							Ver Projeto
						</a>
					{/if}
					{#if project.githubUrl}
						<a 
							href={project.githubUrl}
							target="_blank"
							rel="noopener noreferrer"
							class="flex-1 min-w-[200px] px-6 py-3 bg-gray-900 text-white rounded-lg font-medium text-center hover:bg-gray-800 transition-colors flex items-center justify-center gap-2 no-underline"
						>
							<svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
								<path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
							</svg>
							Ver Código
						</a>
					{/if}
				</div>
			</div>
		</div>
	</div>
{/if}

<style>
	/* Custom scrollbar for modal - matching page style */
	:global(.bg-white.rounded-2xl::-webkit-scrollbar) {
		width: 10px;
	}

	:global(.bg-white.rounded-2xl::-webkit-scrollbar-track) {
		background: rgba(0, 0, 0, 0.04);
		border-radius: 10px;
	}

	:global(.bg-white.rounded-2xl::-webkit-scrollbar-thumb) {
		background: rgba(0, 0, 0, 0.2);
		border-radius: 10px;
		border: 2px solid rgba(0, 0, 0, 0.04);
		transition: background 0.2s ease;
	}

	:global(.bg-white.rounded-2xl::-webkit-scrollbar-thumb:hover) {
		background: rgba(0, 0, 0, 0.35);
	}

	:global(.bg-white.rounded-2xl::-webkit-scrollbar-thumb:active) {
		background: rgba(0, 0, 0, 0.5);
	}
</style>
