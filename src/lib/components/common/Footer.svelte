<script lang="ts">
	const year = new Date().getFullYear();

	const socialLinks = [
		{
			name: 'GitHub',
			url: 'https://github.com/gustavodslara/gustavodslara.github.io',
			icon: 'github'
		},
		{ name: 'LinkedIn', url: 'https://www.linkedin.com/in/gustavodslara/', icon: 'linkedin' }
		// { name: 'Instagram', url: 'https://www.instagram.com/gus.dsl/', icon: 'instagram' }
	];
</script>

<footer
	class="w-full bg-gradient-to-b from-transparent to-black/[0.02] mt-16 px-4 md:px-8 lg:px-12"
>
	<div class="max-w-7xl mx-auto">
		<div class="h-12"></div>

		<!-- Footer Top -->
		<div
			class="flex flex-col md:flex-row items-start md:items-center justify-between gap-6 md:gap-8"
		>
			<div>
				<p class="text-sm md:text-base text-black/60 m-0">
					Desenvolvido em <a
						href="https://kit.svelte.dev"
						target="_blank"
						rel="noopener"
						class="text-black underline hover:text-[#dd206b]">SvelteKit</a
					>
					com
					<a
						href="https://www.typescriptlang.org"
						target="_blank"
						rel="noopener"
						class="text-black underline hover:text-[#dd206b]">TypeScript</a
					>,
					<a
						href="https://tailwindcss.com"
						target="_blank"
						rel="noopener"
						class="text-black underline hover:text-[#dd206b]">TailwindCSS</a
					>
				</p>
			</div>

			<!-- <nav class="flex gap-6 md:gap-8">
				<a href="/" class="text-sm md:text-base font-medium text-black/70 no-underline transition-all duration-200 hover:text-[#dd206b] hover:-translate-y-0.5">
					Icons
				</a>
				<a href="/" class="text-sm md:text-base font-medium text-black/70 no-underline transition-all duration-200 hover:text-[#dd206b] hover:-translate-y-0.5">
					Logos
				</a>
				<a href="/" class="text-sm md:text-base font-medium text-black/70 no-underline transition-all duration-200 hover:text-[#dd206b] hover:-translate-y-0.5">
					Platforms
				</a>
			</nav> -->
		</div>

		<div class="h-14"></div>

		<!-- Footer Bottom -->
		<div
			class="flex flex-col md:flex-row items-start md:items-center justify-between gap-6 md:gap-8"
		>
			<p class="text-sm text-black/50 m-0">
				© {year} Copyright | Gustavo Lara | All rights reserved.
			</p>

			<div class="flex gap-8 md:gap-10">
				{#each socialLinks as social}
					<a
						href={social.url}
						target="_blank"
						rel="noopener"
						aria-label={social.name}
						class="flex items-center justify-center w-10 h-10 rounded-full transition-all duration-300 hover:bg-black/5 hover:-translate-y-1 no-underline"
					>
						<img
							src="/assets/svg/icons/social/{social.icon}.svg"
							alt={social.name}
							class="w-4 h-4 opacity-60 transition-opacity duration-300 hover:opacity-100"
						/>
					</a>
				{/each}
			</div>
		</div>

		<div class="h-5"></div>
	</div>
</footer>
