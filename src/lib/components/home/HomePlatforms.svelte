<script lang="ts">
	import { onMount } from 'svelte';

	let visible = false;

	onMount(() => {
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) visible = true;
			},
			{ threshold: 0.1 }
		);

		const el = document.querySelector('.home-platforms');
		if (el) observer.observe(el);

		return () => observer.disconnect();
	});
</script>

<div class="home-platforms relative z-20 pt-0 pb-8 md:pt-0 md:pb-16 px-4 md:px-8 lg:px-12 bg-white">
	<div class="max-w-7xl mx-auto">
		<!-- Coursera Platform Card -->
		<a
			href="https://abcdario.online"
			target="_blank"
			rel="noopener"
			class="block relative rounded-xl overflow-hidden bg-gradient-to-br from-blue-50 to-indigo-50 no-underline text-black transition-all duration-600 hover:-translate-y-2 hover:shadow-2xl"
			class:opacity-100={visible}
			class:translate-y-0={visible}
			class:opacity-0={!visible}
			class:translate-y-10={!visible}
		>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-6 md:gap-8 p-6 md:p-12 items-center">
				<div class="text-content">
					<h3 class="text-3xl md:text-4xl font-medium mb-4">abcdario.online</h3>
					<p class="text-base md:text-lg leading-relaxed text-black/75 mb-6">
						Cursos didáticos e acessíveis para introdução à programação, modelagem 3D,
						desenvolvimento de jogos, edição de imagem e vídeo, e dicas de carreira. Tornando a
						educação em tecnologia acessível para todos.
					</p>
					<button
						class="bg-[#dd206b] text-white border-none px-8 py-3 rounded font-medium transition-all duration-300 hover:bg-[#c01252] hover:-translate-y-0.5"
					>
						CONHECER PLATAFORMA
					</button>
				</div>
				<div class="flex items-center justify-center">
					<img
						src="/assets/img/illustrations/abcdario.png"
						alt="abcdario.online"
						class="max-w-full h-auto"
					/>
				</div>
			</div>
		</a>

		<div class="h-8"></div>

		<a
			href="https://unrender.games"
			target="_blank"
			rel="noopener"
			class="block relative rounded-xl overflow-hidden bg-gradient-to-br from-purple-50 to-pink-50 no-underline text-black transition-all duration-600 delay-100 hover:-translate-y-2 hover:shadow-2xl"
			class:opacity-100={visible}
			class:translate-y-0={visible}
			class:opacity-0={!visible}
			class:translate-y-10={!visible}
		>
			<div class="grid grid-cols-1 md:grid-cols-2 gap-6 md:gap-8 p-6 md:p-12 items-center">
				<div class="text-content">
					<h3 class="text-3xl md:text-4xl font-medium mb-4">Game Studio</h3>
					<p class="text-base md:text-lg leading-relaxed text-black/75 mb-6">
						Estúdio de jogos especializado em jogos VR e experiências imersivas de realidade
						virtual. Criando entretenimento de realidade virtual de próxima geração.
					</p>
					<button
						class="bg-[#dd206b] text-white border-none px-8 py-3 rounded font-medium transition-all duration-300 hover:bg-[#c01252] hover:-translate-y-0.5"
					>
						NOSSOS PROJETOS
					</button>
				</div>
				<div class="flex items-center justify-center">
					<img
						src="/assets/img/illustrations/unrender.png"
						alt="Unrender Games Illustration"
						class="max-w-full h-auto"
					/>
				</div>
			</div>
		</a>

		<div class="h-8"></div>

		<!-- Cloud Game Saves Platform Card -->
		<a
			href="https://memorycard.digital/"
			target="_blank"
			rel="noopener"
			class="block relative rounded-xl overflow-hidden bg-gradient-to-br from-green-50 to-emerald-50 no-underline text-black transition-all duration-600 delay-200 hover:-translate-y-2 hover:shadow-2xl"
			class:opacity-100={visible}
			class:translate-y-0={visible}
			class:opacity-0={!visible}
			class:translate-y-10={!visible}
		>
			<!-- Open Source Ribbon -->
			<div class="absolute top-0 right-0 z-10 w-[150px] h-[150px] overflow-hidden">
				<span
					class="block absolute w-[200px] py-2 bg-green-500 text-white text-center text-sm rotate-45 top-[30px] -right-[50px] shadow-lg"
				>
					Open Source
				</span>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 gap-6 md:gap-8 p-6 md:p-12 items-center">
				<div class="text-content">
					<h3 class="text-3xl md:text-4xl font-medium mb-4">memorycard.digital</h3>
					<p class="text-base md:text-lg leading-relaxed text-black/75 mb-6">
						Backup automático em nuvem para salvamentos de jogos em todas as plataformas, lojas e
						emuladores. Solução open source para nunca mais perder seu progresso nos jogos.
					</p>
					<button
						class="bg-[#dd206b] text-white border-none px-8 py-3 rounded font-medium transition-all duration-300 hover:bg-[#c01252] hover:-translate-y-0.5"
					>
						TESTE AGORA
					</button>
				</div>
				<div class="flex items-center justify-center">
					<img
						src="/assets/img/illustrations/memorycard-digital.png"
						alt="Cloud Game Saves Illustration"
						class="max-w-full h-auto"
					/>
				</div>
			</div>
		</a>
	</div>
</div>
