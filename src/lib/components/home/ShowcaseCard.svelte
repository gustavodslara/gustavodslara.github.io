<script lang="ts">
	export let name: string;
	export let description: string; // Kept for compatibility but not used in display
	export let stackImages: string[] = [];
	export let stackImageNames: string[] = []; // names for the stackImages (same length as stackImages)
	export let backgroundColor: string = '#ffffff';
	export let phoneImages: string[] = [];
	export let onClick: () => void = () => {};
	export let onImageClick: (imageSrc: string) => void = () => {};
	export let titleColor: string = '#ffffff';
	export let type: 'mobile' | 'desktop' | 'desktop-left' = 'mobile';

	// Fallback for phone images if less than 2 are provided
	$: displayPhoneImages = [
		phoneImages[0] || '/assets/img/placeholder-phone.png',
		phoneImages[1] || phoneImages[0] || '/assets/img/placeholder-phone.png'
	];

	function handleImageClick(e: MouseEvent, src: string) {
		e.stopPropagation();
		onImageClick(src);
	}
</script>

<div
	class="group relative w-full rounded-3xl overflow-hidden text-left transition-all duration-500 hover:shadow-2xl border-none cursor-pointer p-0"
	style="background-color: {backgroundColor}; aspect-ratio: 4/3;"
	on:click={onClick}
	role="button"
	tabindex="0"
	on:keydown={(e) => e.key === 'Enter' && onClick()}
	title={description || name}
>
	<div class="absolute inset-0 flex flex-col justify-between p-6 md:p-8 z-10">
		<!-- Top Section: Stack Logos (Left) & Content -->
		<div class="flex items-start justify-between h-full">
			<!-- Left Column: Stack Logos -->
			<div class="flex flex-col gap-2 md:gap-3 z-20 pointer-events-none">
				{#each stackImages.slice(0, 4) as logo, i}
					<div
						class="w-8 h-8 md:w-10 md:h-10 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center p-1.5 md:p-2 shadow-sm transition-transform hover:scale-110 pointer-events-auto"
					>
						<img
							src={logo}
							alt={stackImageNames[i] || 'Tech'}
							title={stackImageNames[i] || 'Tech'}
							class="w-full h-full object-contain"
						/>
					</div>
				{/each}
				{#if stackImages.length > 4}
					<div
						class="w-8 h-8 md:w-10 md:h-10 bg-white/20 backdrop-blur-sm rounded-full flex items-center justify-center p-1.5 md:p-2 shadow-sm text-xs font-medium text-gray-800 pointer-events-auto"
						title={stackImageNames.slice(4).join(', ')}
						aria-label={stackImageNames.slice(4).join(', ')}
					>
						+{stackImages.length - 4}
					</div>
				{/if}
			</div>

			<!-- Phones Container (Right/Center) -->
			<div
				class="absolute inset-0 flex items-center justify-center pointer-events-none overflow-hidden"
			>
				<!-- Phone 1 (Right) -->
				<button
					class="absolute transform transition-all duration-500 hover:scale-105 brightness-90 hover:brightness-100 pointer-events-auto cursor-zoom-in border-none bg-transparent p-0
					{type === 'desktop-left' ? 'z-20' : ''}
					{type === 'mobile'
						? 'translate-x-12 translate-y-0 rotate-[12deg] hover:translate-y-2 hover:rotate-[15deg] w-[30%] md:w-[25%] max-h-[65%]'
						: type === 'desktop-left'
							? 'translate-x-12 translate-y-6 rotate-[12deg] hover:translate-y-4 hover:rotate-[15deg] w-[30%] md:w-[25%] max-h-[60%]'
							: 'translate-x-8 translate-y-4 rotate-[6deg] hover:translate-y-6 hover:rotate-[8deg] w-[60%] md:w-[55%] max-h-[80%]'}"
					on:click={(e) => handleImageClick(e, displayPhoneImages[1])}
				>
					<img
						src={displayPhoneImages[1]}
						alt="{name} Screen 2"
						class="w-full h-full object-contain drop-shadow-2xl {type === 'mobile' ||
						type === 'desktop-left'
							? 'rounded-[1.5rem] md:rounded-[2rem]'
							: 'rounded-xl'}"
					/>
				</button>
				<!-- Phone 2 (Left) -->
				<button
					class="absolute transform transition-all duration-500 hover:scale-110 pointer-events-auto cursor-zoom-in border-none bg-transparent p-0
					{type === 'desktop-left' ? 'z-10' : 'z-10'}
					{type === 'mobile'
						? '-translate-x-8 translate-y-0 rotate-[-12deg] hover:-translate-y-2 hover:rotate-[-15deg] w-[35%] md:w-[30%] max-h-[65%]'
						: type === 'desktop-left'
							? '-translate-x-4 -translate-y-2 rotate-[-6deg] hover:-translate-y-4 hover:rotate-[-8deg] w-[65%] md:w-[60%] max-h-[80%]'
							: '-translate-x-12 translate-y-6 rotate-[-12deg] hover:-translate-y-4 hover:rotate-[-15deg] w-[30%] md:w-[25%] max-h-[60%]'}"
					on:click={(e) => handleImageClick(e, displayPhoneImages[0])}
				>
					<img
						src={displayPhoneImages[0]}
						alt="{name} Screen 1"
						class="w-full h-full object-contain drop-shadow-2xl {type === 'mobile' ||
						type === 'desktop'
							? 'rounded-[1.5rem] md:rounded-[2rem]'
							: 'rounded-xl'}"
					/>
				</button>
			</div>
		</div>

		<!-- Bottom Section: Name -->
		<div class="relative z-20 mt-auto pointer-events-none w-full">
			<h3
				class="text-base sm:text-lg md:text-xl font-semibold mb-0 drop-shadow-md leading-tight line-clamp-2"
				style="color: {titleColor};"
			>
				{name}
			</h3>
		</div>
	</div>

	<!-- Hover Overlay (Optional, for extra focus) -->
	<div
		class="absolute inset-0 bg-black/0 group-hover:bg-black/5 transition-colors duration-300 pointer-events-none"
	></div>
</div>
