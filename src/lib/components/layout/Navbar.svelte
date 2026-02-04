<script lang="ts">
	import { onMount, onDestroy } from 'svelte';

	export let scrollY = 0;
	export let scrollContainer: HTMLElement | null = null;

	let mobileMenuOpen = false;
	let activeSection = 'home';

	$: isScrolled = scrollY > 100;

	const navItems = [
		{ id: 'home', label: 'Início' },
		{ id: 'about', label: 'Sobre' },
		{ id: 'about', label: 'Experiência' },
		{ id: 'education', label: 'Educação' },
		{ id: 'showcases', label: 'Projetos' },
		{ id: 'platforms', label: 'Plataformas' },
		{ id: 'contact', label: 'Contato' }
	];

	function scrollToSection(sectionId: string) {
		const element = document.getElementById(sectionId);
		if (!element) {
			console.warn(`Section with id "${sectionId}" not found`);
			return;
		}

		const wasMobileMenuOpen = mobileMenuOpen;

		// Close mobile menu first
		mobileMenuOpen = false;

		// Calculate position accounting for fixed navbar
		const navbarHeight = 100;

		// Use requestAnimationFrame for smoother execution
		const performScroll = () => {
			if (scrollContainer) {
				// Container scrolling
				const elementTop = element.getBoundingClientRect().top;
				const containerTop = scrollContainer.getBoundingClientRect().top;
				const currentScrollTop = scrollContainer.scrollTop;

				const offsetPosition = currentScrollTop + (elementTop - containerTop) - navbarHeight;

				scrollContainer.scrollTo({
					top: offsetPosition,
					behavior: 'smooth'
				});
			} else {
				// Window scrolling fallback
				const elementPosition = element.getBoundingClientRect().top + window.pageYOffset;
				const offsetPosition = elementPosition - navbarHeight;

				window.scrollTo({
					top: offsetPosition,
					behavior: 'smooth'
				});
			}
		};

		// If mobile menu was open, wait for it to close before scrolling
		if (wasMobileMenuOpen) {
			setTimeout(() => {
				requestAnimationFrame(performScroll);
			}, 300);
		} else {
			requestAnimationFrame(performScroll);
		}
	}

	function updateActiveSection() {
		const sections = navItems.map((item) => item.id);
		const scrollPosition = scrollY + 150; // Offset for better UX

		for (let i = sections.length - 1; i >= 0; i--) {
			const element = document.getElementById(sections[i]);
			if (element) {
				let elementTop = 0;
				
				if (scrollContainer) {
					const rect = element.getBoundingClientRect();
					const containerRect = scrollContainer.getBoundingClientRect();
					elementTop = rect.top - containerRect.top + scrollContainer.scrollTop;
				} else {
					const rect = element.getBoundingClientRect();
					elementTop = rect.top + window.scrollY;
				}

				if (elementTop <= scrollPosition) {
					activeSection = sections[i];
					break;
				}
			}
		}
	}

	$: if (scrollY >= 0) {
		updateActiveSection();
	}

	function handleScroll() {
		scrollY = scrollContainer ? scrollContainer.scrollTop : window.scrollY;
	}

	// Watch for scrollContainer changes to attach/detach listeners
	$: if (scrollContainer) {
		scrollContainer.addEventListener('scroll', handleScroll);
		scrollY = scrollContainer.scrollTop;
		updateActiveSection();
	} else if (typeof window !== 'undefined') {
		// Fallback to window listener if no container provided (and we are in browser)
		window.addEventListener('scroll', handleScroll);
		scrollY = window.scrollY;
		updateActiveSection();
	}

	onDestroy(() => {
		if (scrollContainer) {
			scrollContainer.removeEventListener('scroll', handleScroll);
		}
		if (typeof window !== 'undefined') {
			window.removeEventListener('scroll', handleScroll);
		}
	});
</script>

<nav
	class="fixed top-0 left-0 right-0 z-50 bg-white backdrop-blur-sm transition-all duration-300 px-4 md:px-8 py-3 md:py-4"
	class:shadow-md={isScrolled}
>
	<div class="max-w-7xl mx-auto flex items-center justify-between">
		<!-- Logo -->
		<a
			href="/"
			class="flex items-center no-underline transition-transform duration-200 hover:scale-105"
		>
			<img src="/assets/img/logos/gustavolara.png" alt="NP Logo" class="h-8 md:h-10 w-auto" />
		</a>

		<!-- Desktop Navigation -->
		<div class="hidden lg:flex items-center gap-2">
			{#each navItems as item}
				<button
					on:click={() => scrollToSection(item.id)}
					class="px-4 py-2 rounded-lg text-base font-medium transition-all duration-300 relative group {activeSection ===
					item.id
						? 'text-[#dd206b]'
						: 'text-black/70'}"
				>
					{item.label}
					<span
						class="absolute bottom-1 left-1/2 -translate-x-1/2 h-0.5 bg-[#dd206b] transition-all duration-300 {activeSection ===
						item.id
							? 'w-8'
							: 'w-0'}"
					></span>
					<span
						class="absolute bottom-1 left-1/2 -translate-x-1/2 h-0.5 w-0 bg-[#dd206b]/30 transition-all duration-300 group-hover:w-8 {activeSection ===
						item.id
							? 'hidden'
							: ''}"
					></span>
				</button>
			{/each}
		</div>

		<!-- Mobile Menu Button -->
		<button
			on:click={() => (mobileMenuOpen = !mobileMenuOpen)}
			class="lg:hidden flex flex-col items-center justify-center w-10 h-10 space-y-1.5 focus:outline-none"
			aria-label="Toggle menu"
		>
			<span
				class="w-6 h-0.5 bg-black transition-all duration-300 {mobileMenuOpen
					? 'rotate-45 translate-y-2'
					: ''}"
			></span>
			<span
				class="w-6 h-0.5 bg-black transition-all duration-300 {mobileMenuOpen ? 'opacity-0' : ''}"
			></span>
			<span
				class="w-6 h-0.5 bg-black transition-all duration-300 {mobileMenuOpen
					? '-rotate-45 -translate-y-2'
					: ''}"
			></span>
		</button>
	</div>

	<!-- Mobile Menu -->
	{#if mobileMenuOpen}
		<div
			class="lg:hidden absolute top-full left-0 right-0 bg-white backdrop-blur-sm shadow-lg border-t border-gray-200 animate-slideDown"
		>
			<div class="max-w-7xl mx-auto px-4 py-4 flex flex-col gap-1">
				{#each navItems as item}
					<button
						on:click={() => scrollToSection(item.id)}
						class="text-left px-4 py-3 rounded-lg text-base font-medium transition-all duration-300 {activeSection ===
						item.id
							? 'bg-[#dd206b] text-white'
							: 'text-black hover:bg-gray-100'}"
					>
						{item.label}
					</button>
				{/each}
			</div>
		</div>
	{/if}
</nav>

<style>
	@keyframes slideDown {
		from {
			opacity: 0;
			transform: translateY(-10px);
		}
		to {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.animate-slideDown {
		animation: slideDown 0.2s ease-out forwards;
	}
</style>
