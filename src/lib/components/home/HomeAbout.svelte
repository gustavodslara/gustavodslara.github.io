<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let openJobs: Set<number> = new Set();
	let isMobile = false;

	onMount(() => {
		// Check if mobile
		isMobile = window.innerWidth < 768;

		// Open jobs based on device
		if (isMobile) {
			// On mobile, only first job is open
			openJobs = new Set([1]);
		} else {
			// On desktop, open all non-freelance jobs (1, 3, 5, 7, 8, 9)
			openJobs = new Set([1, 3, 5, 7, 8, 9]);
		}

		// Wait for DOM to be fully ready before initializing animations
		setTimeout(() => {
			// GSAP ScrollTrigger animations with optimized performance
			// Section header animation
			gsap.fromTo(
				'.home-about .flex.items-end.gap-3.mb-6',
				{ opacity: 0, y: 30 },
				{
					opacity: 1,
					y: 0,
					duration: 0.6,
					ease: 'power2.out',
					scrollTrigger: {
						trigger: '.home-about',
						start: 'top 90%',
						end: 'top 30%',
						toggleActions: 'play none play reverse'
					}
				}
			);

			// Content grid animation
			gsap.fromTo(
				'.home-about .grid.grid-cols-1.md\\:grid-cols-2',
				{ opacity: 0, y: 40 },
				{
					opacity: 1,
					y: 0,
					duration: 0.8,
					ease: 'power2.out',
					scrollTrigger: {
						trigger: '.home-about .grid.grid-cols-1.md\\:grid-cols-2',
						start: 'top 85%',
						end: 'top 35%',
						toggleActions: 'play none play reverse'
					}
				}
			);

			// Tech stack items animation with reduced stagger for performance
			gsap.fromTo(
				'.home-about .flex.flex-wrap.gap-2 a',
				{ opacity: 0, scale: 0.9, y: 15 },
				{
					opacity: 1,
					scale: 1,
					y: 0,
					duration: 0.5,
					ease: 'back.out(1.5)',
					stagger: 0.02,
					scrollTrigger: {
						trigger: '.home-about .flex.flex-wrap.gap-2',
						start: 'top 88%',
						end: 'top 25%',
						toggleActions: 'play none play reverse'
					}
				}
			);

			// Job experience timeline animation
			gsap.fromTo(
				'.home-about .relative.w-full .relative.mb-6',
				{ opacity: 0, x: -30 },
				{
					opacity: 1,
					x: 0,
					duration: 0.6,
					ease: 'power2.out',
					stagger: 0.08,
					scrollTrigger: {
						trigger: '.home-about .relative.w-full',
						start: 'top 85%',
						end: 'top 40%',
						toggleActions: 'play none play reverse'
					}
				}
			);

			// Expertise section animation
			gsap.fromTo(
				'.home-about .grid.grid-cols-1.md\\:grid-cols-2.gap-4 .p-6',
				{ opacity: 0, y: 25, scale: 0.95 },
				{
					opacity: 1,
					y: 0,
					scale: 1,
					duration: 0.7,
					ease: 'power2.out',
					stagger: 0.08,
					scrollTrigger: {
						trigger: '.home-about .grid.grid-cols-1.md\\:grid-cols-2.gap-4',
						start: 'top 88%',
						end: 'top 30%',
						toggleActions: 'play none play reverse'
					}
				}
			);
		}, 50); // Small delay to ensure DOM is ready
	});

	const expertise = [
		{
			title: 'Sistemas Distribuídos',
			skills: [
				'Arquitetura Hexagonal',
				'Arquitetura Orientada a Eventos',
				'Padrão Saga & Service Mesh',
				'Padrão Circuit Breaker',
				'TDD/BDD',
				'CQRS & Event Sourcing'
			],
			colored: true
		},
		{
			title: 'Desenvolvimento Full-Stack',
			skills: [
				'Web Apps (Angular, Svelte)',
				'Aplicações Híbridas (Ionic, Flutter, Qt, Tauri, Qt)',
				'Apps Nativos (Android/iOS)',
				'Arquitetura Microfrontend',
				'Geração de Sites Estáticos (SSG)',
				'Renderização no Cliente (CSR)'
			]
		},
		{
			title: 'Inteligência Artificial',
			skills: [
				'Agentes Autônomos',
				'Chatbots & IA Conversacional',
				'Visão Computacional',
				'Reconhecimento de Imagem',
				'Análise de Vídeo',
				'Geração de Imagens'
			]
		},
		{
			title: 'IoT & Embarcados',
			skills: [
				'Orange Pi',
				'Zephyr RTOS',
				'Programação Bare Metal',
				'Controle GPIO & Hardware',
				'Sistemas de Casa Inteligente',
				'Reconhecimento de Imagem'
			]
		},
		{
			title: 'Desenvolvimento 3D & Jogos',
			skills: [
				'Modelagem 3D',
				'Retopologia',
				'Animação de Personagens',
				'Documento de Design de Jogos',
				'Design de Níveis',
				'Web, PC, Mobile, AR, VR e MR'
			]
		},
		{
			title: 'Aplicações Nativas',
			skills: [
				'Flutter, Ionic, Qt, Tauri, WinUI, .NET MAUI',
				'Windows, Linux, Mac, Android, iOS e VR',
				'Integração de Hardware',
				'Sensores e Atuadores',
				'Leitores Biométricos',
				'Impressoras Térmicas'
			]
		}
	];

	const techStack = {
		languages: [
			{
				name: 'JavaScript',
				logo: '/assets/img/tools/javascript.png',
				link: 'https://developer.mozilla.org/en-US/docs/Web/JavaScript'
			},
			{
				name: 'TypeScript',
				logo: '/assets/img/tools/typescript.png',
				link: 'https://www.typescriptlang.org/'
			},
			{ name: 'Python', logo: '/assets/img/tools/javascript.png', link: 'https://www.python.org/' },
			{ name: 'Java', logo: '/assets/img/tools/java.png', link: 'https://www.java.com/' },
			{
				name: 'Kotlin',
				logo: '/assets/img/tools/kotlin-logo.png',
				link: 'https://kotlinlang.org/'
			},
			{ name: 'Scala', logo: '/assets/img/tools/scala.png', link: 'https://www.scala-lang.org/' },
			{ name: 'Groovy', logo: '/assets/img/tools/groovy.png', link: 'https://groovy-lang.org/' },
			{ name: 'Swift', logo: '/assets/img/tools/swift.png', link: 'https://swift.org/' },
			{ name: 'Golang', logo: '/assets/img/tools/golang.png', link: 'https://go.dev/' },
			{ name: 'Rust', logo: '/assets/img/tools/rust.png', link: 'https://www.rust-lang.org/' },
			{
				name: 'C',
				logo: '/assets/img/tools/c.png',
				link: 'https://en.wikipedia.org/wiki/C_(programming_language)'
			},
			{ name: 'C++', logo: '/assets/img/tools/c++.png', link: 'https://isocpp.org/' }
		],
		frontend: [
			{
				name: 'Angular',
				logo: '/assets/img/tools/angular.png',
				link: 'https://angular.io/',
				color: '#DD0031'
			},
			{
				name: 'NgRx',
				logo: '/assets/img/tools/ngrx.svg',
				link: 'https://ngrx.io/',
				color: '#BA2BD2'
			},
			{
				name: 'Svelte',
				logo: '/assets/img/tools/svelte.png',
				link: 'https://svelte.dev/'
			},
			{ name: 'Ionic', logo: '/assets/img/tools/ionic.png', link: 'https://ionicframework.com/' },
			{
				name: 'Tailwind CSS',
				logo: '/assets/img/tools/tailwind.png',
				link: 'https://tailwindcss.com/'
			},
			{
				name: 'Sass',
				logo: '/assets/img/tools/sass-logo.svg',
				link: 'https://sass-lang.com/',
				color: '#CC6699'
			},
			{
				name: 'Flutter',
				logo: '/assets/img/tools/flutter_logo.svg',
				link: 'https://flutter.dev/',
				color: '#02569B'
			},
			{
				name: 'Android',
				logo: '/assets/img/tools/android.svg',
				link: 'https://developer.android.com/',
				color: '#3DDC84'
			},
			{
				name: 'Jetpack Compose',
				logo: '/assets/img/tools/pic_jetpack_compose.png',
				link: 'https://developer.android.com/jetpack/compose'
			},
			{
				name: 'SwiftUI',
				logo: '/assets/img/tools/swiftui.png',
				link: 'https://developer.apple.com/xcode/swiftui/'
			},
			{ name: 'Qt', logo: '/assets/img/tools/qt.png', link: 'https://www.qt.io/' },
			{ name: 'LVGL', logo: '/assets/img/tools/lvgl.png', link: 'https://lvgl.io/' },
			{ name: 'Tauri', logo: '/assets/img/tools/tauri.png', link: 'https://tauri.app/' },
			{ name: 'D3.js', logo: '/assets/img/tools/d3.svg', link: 'https://d3js.org/' },
			{
				name: 'Highcharts',
				logo: '/assets/img/tools/highchart-logo.png',
				link: 'https://www.highcharts.com/'
			},
			{ name: 'Chart.js', logo: '/assets/img/tools/chartjs.png', link: 'https://www.chartjs.org/' }
		],
		backend: [
			{ name: 'Node.js', logo: '/assets/img/tools/nodejs.png', link: 'https://nodejs.org/' },
			{ name: 'Express', logo: '/assets/img/tools/express.png', link: 'https://expressjs.com/' },
			{ name: 'NestJS', logo: '/assets/img/tools/nestjs.png', link: 'https://nestjs.com/' },
			{ name: 'Prisma', logo: '/assets/img/tools/prisma.png', link: 'https://www.prisma.io/' },
			{
				name: 'Sequelize',
				logo: '/assets/img/tools/sequelize.png',
				link: 'https://sequelize.org/'
			},
			{
				name: 'Spring Boot',
				logo: '/assets/img/tools/springboot.png',
				link: 'https://spring.io/projects/spring-boot'
			},
			{ name: 'Quarkus', logo: '/assets/img/tools/quarkus.png', link: 'https://quarkus.io/' },
			{
				name: 'Micronaut',
				logo: '/assets/img/tools/micronaut.png',
				link: 'https://micronaut.io/',
				color: '#000000'
			},
			{ name: 'Helidon', logo: '/assets/img/tools/helidon.png', link: 'https://helidon.io/' },
			{ name: 'Fiber', logo: '/assets/img/tools/golang.png', link: 'https://gofiber.io/' },
			{ name: 'gRPC', logo: '/assets/img/tools/grpc.png', link: 'https://grpc.io/' }
		],
		databases: [
			{
				name: 'PostgreSQL',
				logo: '/assets/img/tools/postgres.png',
				link: 'https://www.postgresql.org/'
			},
			{ name: 'MySQL', logo: '/assets/img/tools/mysql.png', link: 'https://www.mysql.com/' },
			{
				name: 'Oracle DB',
				logo: '/assets/img/tools/oracledb.png',
				link: 'https://www.oracle.com/database/'
			},
			{ name: 'MongoDB', logo: '/assets/img/tools/mongodb.png', link: 'https://www.mongodb.com/' },
			{ name: 'Redis', logo: '/assets/img/tools/redis.png', link: 'https://redis.io/' },
			{ name: 'Neo4j', logo: '/assets/img/tools/neo4j.png', link: 'https://neo4j.com/' },
			{
				name: 'ChromaDB',
				logo: '/assets/img/tools/chromadb.png',
				link: 'https://www.trychroma.com/'
			},
			{
				name: 'Firebase',
				logo: '/assets/img/tools/firebase.png',
				link: 'https://firebase.google.com/'
			}
		],
		cloud: [
			{ name: 'Docker', logo: '/assets/img/tools/docker.png', link: 'https://www.docker.com/' },
			{
				name: 'Kubernetes',
				logo: '/assets/img/tools/kubernetes.png',
				link: 'https://kubernetes.io/'
			},
			{
				name: 'Terraform',
				logo: '/assets/img/tools/terraform.png',
				link: 'https://www.terraform.io/'
			},
			{ name: 'AWS', logo: '/assets/img/tools/aws.png', link: 'https://aws.amazon.com/' },
			{ name: 'Azure', logo: '/assets/img/tools/azure.png', link: 'https://azure.microsoft.com/' },
			{
				name: 'Google Cloud',
				logo: '/assets/img/tools/google-cloud.png',
				link: 'https://cloud.google.com/'
			},
			{ name: 'Kafka', logo: '/assets/img/tools/kafka.png', link: 'https://kafka.apache.org/' },
			{
				name: 'RabbitMQ',
				logo: '/assets/img/tools/rabbitmq.png',
				link: 'https://www.rabbitmq.com/'
			},
			{ name: 'GitHub', logo: '/assets/img/tools/github.png', link: 'https://github.com/' },
			{ name: 'Maven', logo: '/assets/img/tools/maven.png', link: 'https://maven.apache.org/' },
			{ name: 'Gradle', logo: '/assets/img/tools/gradle.png', link: 'https://gradle.org/' },
			{
				name: 'ELK Stack',
				logo: '/assets/img/tools/elk stack.png',
				link: 'https://www.elastic.co/elastic-stack'
			},
			{
				name: 'SonarQube',
				logo: '/assets/img/tools/sonarqube.png',
				link: 'https://www.sonarqube.org/'
			}
		],
		ai: [
			{
				name: 'FastAPI',
				logo: '/assets/img/tools/fastapi.png',
				link: 'https://fastapi.tiangolo.com/'
			},
			{ name: 'PyTorch', logo: '/assets/img/tools/pytorch.png', link: 'https://pytorch.org/' },
			{
				name: 'TensorFlow',
				logo: '/assets/img/tools/tensorflow.png',
				link: 'https://www.tensorflow.org/'
			},
			{
				name: 'TensorFlow.js',
				logo: '/assets/img/tools/tensorflowjs.png',
				link: 'https://www.tensorflow.org/js'
			},
			{
				name: 'LangChain',
				logo: '/assets/img/tools/langchain.png',
				link: 'https://www.langchain.com/'
			},
			{
				name: 'LlamaIndex',
				logo: '/assets/img/tools/llamaindex.png',
				link: 'https://www.llamaindex.ai/'
			},
			{ name: 'Ollama', logo: '/assets/img/tools/ollama.png', link: 'https://ollama.ai/' },
			{
				name: 'MCP Server',
				logo: '/assets/img/tools/mcpserver.png',
				link: 'https://modelcontextprotocol.io/'
			},
			{ name: 'OpenCV', logo: '/assets/img/tools/opencv.png', link: 'https://opencv.org/' },
			{ name: 'Pandas', logo: '/assets/img/tools/pandas.png', link: 'https://pandas.pydata.org/' },
			{ name: 'NumPy', logo: '/assets/img/tools/numpy.png', link: 'https://numpy.org/' },
			{ name: 'MQTT', logo: '/assets/img/tools/mqtt.png', link: 'https://mqtt.org/' }
		],
		tools: [
			{ name: 'Git', logo: '/assets/img/tools/git.png', link: 'https://git-scm.com/' },
			{
				name: 'VS Code',
				logo: '/assets/img/tools/vscode.png',
				link: 'https://code.visualstudio.com/'
			},
			{
				name: 'IntelliJ IDEA',
				logo: '/assets/img/tools/intellij.png',
				link: 'https://www.jetbrains.com/idea/'
			},
			{
				name: 'DataGrip',
				logo: '/assets/img/tools/datagrip.png',
				link: 'https://www.jetbrains.com/datagrip/'
			},
			{
				name: 'Figma',
				logo: '/assets/img/tools/figma.svg',
				link: 'https://www.figma.com/',
				color: '#F24E1E'
			},
			{
				name: 'Affinity',
				logo: '/assets/img/tools/affinity.png',
				link: 'https://affinity.serif.com/'
			},
			{ name: 'GIMP', logo: '/assets/img/tools/gimp.png', link: 'https://www.gimp.org/' },
			{ name: 'Inkscape', logo: '/assets/img/tools/inkscape.png', link: 'https://inkscape.org/' }
		],
		gamedev: [
			{ name: 'Unity', logo: '/assets/img/tools/unity.png', link: 'https://unity.com/' },
			{
				name: 'Unreal Engine',
				logo: '/assets/img/tools/unreal.png',
				link: 'https://www.unrealengine.com/'
			},
			{ name: 'Blender', logo: '/assets/img/tools/blender.png', link: 'https://www.blender.org/' },
			{ name: 'Three.js', logo: '/assets/img/tools/threejs.png', link: 'https://threejs.org/' },
			{
				name: 'Babylon.js',
				logo: '/assets/img/tools/babylonjs.png',
				link: 'https://www.babylonjs.com/'
			},
			{ name: 'p5.js', logo: '/assets/img/tools/p5js.png', link: 'https://p5js.org/' }
		]
	};

	interface JobExperience {
		id: number;
		company: string;
		logo: string;
		title: string;
		startDate: string;
		endDate: string;
		color: string;
		description: string | string[];
		isFreelance?: boolean;
	}

	const experiences: JobExperience[] = [
		{
			id: 1,
			company: 'QIMA',
			logo: '/assets/img/logos/qima_logo.png',
			title: 'Engenheiro de Software',
			startDate: 'Set 2024',
			endDate: 'Out 2025',
			color: '#DD206B',
			description: [
				'Colaborei com uma equipe internacional em uma migração de um sistema legado (PHP, MySQL), automatizando os processos manuais do backoffice. Implementei um microfrontend Angular, um BFF em Quarkus Native e agentes de IA em Python (gRPC).',
				'Com isso conseguimos 80% menos latência, um consumo 60% menor de recursos e queda de tempo para emitir certificados caiu de horas para minutos, 95% dos erros manuais foram eliminados.'
			]
		},
		{
			id: 2,
			company: 'Umbler',
			logo: '/assets/img/logos/umbler.jpg',
			title: 'Arquiteto de Software',
			startDate: 'Jun 2024',
			endDate: 'Out 2024',
			color: '#FF6B35',
			description:
				'Liderei a arquitetura e o desenvolvimento de um agente de IA (Python, FastAPI, RAG) para atendimento, garantindo a excelência técnica e o alinhamento do roadmap com os objetivos.',
			isFreelance: true
		},
		{
			id: 3,
			company: 'MamInfo',
			logo: '/assets/img/logos/maminfo_logo.png',
			title: 'Líder Técnico',
			startDate: 'Mai 2022',
			endDate: 'Jul 2024',
			color: '#9C27B0',
			description: [
				'Liderei a arquitetura e desenvolvimento de uma plataforma de pós-vendas modular e de múltiplas tecnologias (.NET, Spring Boot). Defini a arquitetura de microservices e microfrontends Angular, todo o CI/CD (GitHub Actions) e usei IaC (Terraform) para publicação em produção na AWS (EC2).',
				'Além do planejamento das sprints e do refinamento técnico do backlog, eu mentor e tive uma mão na solução dos desafios mais complexos, garantindo a qualidade e a evolução contínua do projeto.'
			]
		},
		{
			id: 4,
			company: 'Totem TI',
			logo: '/assets/img/logos/totemti_logo.png',
			title: 'Desenvolvedor Full Stack',
			startDate: 'Jun 2022',
			endDate: '1 sprint',
			color: '#FF9500',
			description:
				'Atuei em um sprint de manutenção em um sistema legado (Java 6, JSF, JBoss Seam, Oracle) para o MPMA, focado na atualização de telas e correção de bugs críticos.',
			isFreelance: true
		},
		{
			id: 5,
			company: 'Accenture Brasil',
			logo: '/assets/img/logos/accenture_logo.png',
			title: 'Desenvolvedor sênior',
			startDate: 'Mai 2021',
			endDate: 'Mai 2022',
			color: '#F57FFF',
			description: [
				'Atuei na migração de sistemas bancários, middlewares usados por caixas eletrônicos (Spring 3) para microservices em Java 11 com Spring Boot Webflux, jPOS, ISO-8583, Apache Kafka e Redis.',
				'Participei também da migração do frontend dos caixas eletrônicos de Windows/JAM (Framework da Diebold baseado em Java Swing) para Linux Yocto com Qt e Rust, integrando com os microservices.'
			]
		},
		{
			id: 6,
			company: 'ArloesiTech',
			logo: '/assets/img/logos/arloesitech_logo.png',
			title: 'Desenvolvedor de aplicativos',
			startDate: 'Ago 2021',
			endDate: '1 sprint',
			color: '#00C9A7',
			description:
				'Entreguei o MVP de um aplicativo de restaurante (Flutter), definindo a arquitetura de estado com MobX em um sprint de rápida prototipação e entrega.',
			isFreelance: true
		},
		{
			id: 7,
			company: 'TCE-MT',
			logo: '/assets/img/logos/tcemt_logo.png',
			title: 'Desenvolvedor pleno',
			startDate: 'Jan 2020',
			endDate: 'Mai 2021',
			color: '#027DFD',
			description: [
				'Participei da modernização de um sistema legado de auditoria (Delphi, Oracle Procedures) para uma arquitetura de microserviços (Java 11, Kotlin, Spring Boot) com comunicação via Spring Cloud (OpenFeign).',
				'Desenvolvi rotinas de processamento assíncrono (Kafka, Spring Batch), criei processos de ETL e na integração com OCR (Tess4J) e bibliotecas nativas legadas (JNI, JNA).'
			]
		},
		{
			id: 8,
			company: 'Ábaco Tecnologia',
			logo: '/assets/img/logos/abaco_logo.png',
			title: 'Desenvolvedor júnior',
			startDate: 'Jan 2019',
			endDate: 'Jan 2020',
			color: '#68F17E',
			description: [
				'Atuei no desenvolvimento de um app de gestão educacional (Ionic 3, Angular 4, Cordova), construído para atender a uma licitação e adaptado para outro cliente.',
				'Implementei uma arquitetura offline-first (SQLite, NgRx) com Lazy Loading, e automatizei builds e publicação na App Store/Google Play com (Jenkins, Fastlane).'
			]
		},
		{
			id: 9,
			company: 'Totem TI',
			logo: '/assets/img/logos/totemti_logo.png',
			title: 'Desenvolvedor júnior',
			startDate: 'Mar 2018',
			endDate: 'Dez 2018',
			color: '#FFD647',
			description: [
				'Atuei em um ERP/PDV (Java Swing, MySQL) e dashboard de BI (Angular, Spring Boot, MongoDB).',
				'Trabalhei com emissão de NFe (JAX-WS, XML-DSig), processos de ETL, integração com hardware (.dll) via JNI/JNA e distribuição com Java Web Start (JNLP).'
			]
		}
	];

	function toggleJob(id: number) {
		if (openJobs.has(id)) {
			openJobs.delete(id);
		} else {
			openJobs.add(id);
		}
		openJobs = openJobs; // Trigger reactivity
	}
</script>

<div id="about" class="home-about py-8 md:py-16 px-4 md:px-8 lg:px-12">
	<!-- Section Header -->
	<div class="mb-6 md:mb-8">
		<h2 class="text-3xl md:text-4xl font-medium whitespace-nowrap">Sobre Mim</h2>
	</div>

	<div class="max-w-7xl mx-auto">
		<!-- Content Grid -->
		<div class="grid grid-cols-1 md:grid-cols-2 gap-8 md:gap-12">
			<!-- Left Content -->
			<div class="flex flex-col">
				<div class="h-12 md:h-16"></div>

				<p class="text-base md:text-lg leading-relaxed text-black/70 mb-3 md:mb-4">
					Do Brasil, me especializei em <strong class="text-black font-medium"
						>arquitetura de sistemas distribuídos</strong
					>
					e <strong class="text-black font-medium">desenvolvimento fullstack</strong>. Arquitetei e
					entreguei <strong class="text-black font-medium">plataformas de microserviços</strong>
					processando milhões de requisições,
					<strong class="text-black font-medium">aplicações mobile</strong> para Android e iOS, e
					<strong class="text-black font-medium">aplicações web modernas</strong> usando Angular e Svelte.
				</p>

				<p class="text-base md:text-lg leading-relaxed text-black/70 mb-8 md:mb-14">
					Meu foco está na construção de sistemas distribuídos resilientes e escaláveis com
					arquiteturas orientadas a eventos, implementação de pipelines CI/CD, e liderança de
					equipes de engenharia para entregar software de alta qualidade que possa escalar e evoluir
					com as necessidades do negócio.
				</p>

				<!-- Stats -->
				<div class="flex flex-wrap gap-8 md:gap-12 mb-8 md:mb-14">
					<div>
						<h2 class="text-4xl md:text-5xl font-extralight mb-3">7+</h2>
						<h4 class="text-lg md:text-xl font-normal">Anos de Experiência</h4>
					</div>
					<div>
						<h2 class="text-4xl md:text-5xl font-extralight mb-3">20+</h2>
						<h4 class="text-lg md:text-xl font-normal">Projetos Entregues</h4>
					</div>
				</div>

				<!-- Download CV Button -->
				<a
					href="https://github.com/gustavodslara/gustavodslara.github.io/raw/refs/heads/master/cv-gusdsl-ptbr.pdf"
					target="_blank"
					rel="noopener"
					class="inline-block self-start bg-[#dd206b] text-white px-8 py-3 rounded transition-all duration-300 font-medium shadow-[0_2px_8px_rgba(221,32,107,0.3)] hover:bg-[#c01252] hover:-translate-y-0.5 hover:shadow-[0_4px_12px_rgba(221,32,107,0.4)] no-underline"
				>
					Baixar CV
				</a>

				<!-- Tech Stack Section - Below CV Button -->
				<div class="mt-8 md:mt-12">
					<div class="flex items-end gap-3 mb-4 md:mb-6">
						<h4 class="text-xl md:text-2xl font-normal whitespace-nowrap">Stack</h4>
					</div>

					<!-- Languages -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">Linguagens</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.languages as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline bg-gray-100 text-black whitespace-nowrap"
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>

					<!-- Frontend -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">Frontend</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.frontend as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline whitespace-nowrap"
									class:bg-gray-100={!tool.color}
									class:text-black={!tool.color}
									class:text-white={tool.color}
									style={tool.color ? `background-color: ${tool.color};` : ''}
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>

					<!-- Backend -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">Backend</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.backend as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline fade-in whitespace-nowrap"
									class:bg-gray-100={!tool.color}
									class:text-black={!tool.color}
									class:text-white={tool.color}
									style="{tool.color
										? `background-color: ${tool.color};`
										: ''} animation-delay: {1.1 + i * 0.03}s;"
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>

					<!-- Databases -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">Bancos de Dados</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.databases as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline bg-gray-100 text-black whitespace-nowrap"
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>

					<!-- Cloud -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">Nuvem</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.cloud as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline bg-gray-100 text-black whitespace-nowrap"
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>

					<!-- AI & Data -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">IA & Dados</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.ai as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline bg-gray-100 text-black fade-in whitespace-nowrap"
									style="animation-delay: {1.5 + i * 0.03}s;"
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>

					<!-- Tools -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">Ferramentas</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.tools as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline fade-in whitespace-nowrap"
									class:bg-gray-100={!tool.color}
									class:text-black={!tool.color}
									class:text-white={tool.color}
									style="{tool.color
										? `background-color: ${tool.color};`
										: ''} animation-delay: {1.6 + i * 0.03}s;"
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>

					<!-- Game Development & 3D -->
					<div class="mb-6">
						<h5 class="text-sm md:text-base font-semibold mb-3 text-gray-600">
							Desenvolvimento de Jogos & 3D
						</h5>
						<div class="flex flex-wrap gap-2 md:gap-3 justify-start">
							{#each techStack.gamedev as tool, i}
								<a
									href={tool.link}
									target="_blank"
									rel="noopener"
									class="flex items-center gap-2 px-3 md:px-4 py-2 rounded-lg transition-all duration-300 hover:scale-105 hover:shadow-lg no-underline fade-in whitespace-nowrap bg-gray-100 text-black"
									style="animation-delay: {1.7 + i * 0.03}s;"
								>
									<img
										src={tool.logo}
										alt={tool.name}
										class="h-4 md:h-5 w-auto object-contain"
										style="max-height: 20px; max-width: 100px;"
									/>
									<span class="text-xs md:text-sm font-medium">{tool.name}</span>
								</a>
							{/each}
						</div>
					</div>
				</div>
			</div>

			<!-- Right: Job Experience Timeline -->
			<div class="relative flex flex-col items-start mt-8 md:mt-0 pl-4 md:pl-8">
				<div class="mb-6">
					<h3 class="text-2xl md:text-3xl font-normal text-black mb-2">Experiência</h3>
					<p class="text-sm text-black/60">Clique para explorar minha trajetória</p>
				</div>

				<!-- Timeline Branch Structure -->
				<div class="relative w-full">
					<!-- Vertical Line -->
					<div
						class="absolute left-6 top-0 bottom-0 w-0.5 bg-gradient-to-b from-[#dd206b] via-[#667eea] to-[#FFD647]"
					></div>

					<!-- Experience Nodes -->
					{#each experiences as exp, i}
						<div
							class="relative mb-6 pl-16 cursor-pointer group"
							style="animation-delay: {0.8 + i * 0.08}s;"
							on:click={() => toggleJob(exp.id)}
							on:keydown={(e) => e.key === 'Enter' && toggleJob(exp.id)}
							role="button"
							tabindex="0"
						>
							<!-- Branch Line -->
							<div
								class="absolute left-6 top-4 w-10 h-0.5 transition-all duration-300 group-hover:w-12"
								style="background: {exp.color};"
								class:border-dashed={exp.isFreelance}
							></div>

							<!-- Node Circle -->
							<div
								class="absolute left-4 top-2 w-5 h-5 rounded-full border-2 flex items-center justify-center transition-all duration-300 transform group-hover:scale-125 shadow-lg"
								style="background: {openJobs.has(exp.id)
									? exp.color
									: '#fff'}; border-color: {exp.color};"
								class:ring-4={openJobs.has(exp.id)}
								class:ring-opacity-30={openJobs.has(exp.id)}
								class:border-dashed={exp.isFreelance}
								style:--tw-ring-color={exp.color}
							>
								{#if openJobs.has(exp.id)}
									<div class="w-2 h-2 rounded-full bg-white"></div>
								{/if}
							</div>

							<!-- Company Logo Badge -->
							<div
								class="absolute left-0 top-0 w-12 h-12 rounded-full flex items-center justify-center transition-all duration-300 transform group-hover:scale-110 shadow-md overflow-hidden bg-white"
								class:opacity-90={exp.isFreelance}
							>
								<img
									src={exp.logo}
									alt="{exp.company} logo"
									class="w-full h-full object-contain p-1"
								/>
							</div>

							<!-- Job Info Card -->
							<div
								class="bg-white rounded-xl p-4 shadow-md border-2 transition-all duration-300 group-hover:shadow-xl group-hover:-translate-y-1"
								style="border-color: {openJobs.has(exp.id) ? exp.color : 'rgba(0,0,0,0.08)'};"
								class:border-dashed={exp.isFreelance}
							>
								<div class="flex items-start justify-between mb-2">
									<div class="flex-1">
										<div class="flex items-center gap-2 flex-wrap">
											<h4 class="text-base md:text-lg font-medium text-black">{exp.title}</h4>
											{#if exp.isFreelance}
												<span
													class="text-xs px-2 py-0.5 rounded-full font-medium text-white"
													style="background: {exp.color};"
												>
													Freelance
												</span>
											{/if}
										</div>
										<p class="text-sm md:text-base text-black/70 font-medium">{exp.company}</p>
									</div>
									<div
										class="w-6 h-6 rounded-full flex items-center justify-center transition-transform duration-300 flex-shrink-0"
										class:rotate-90={openJobs.has(exp.id)}
										style="background: {exp.color}30;"
									>
										<span style="color: {exp.color};">→</span>
									</div>
								</div>

								<div
									class="flex items-center gap-2 text-xs md:text-sm text-black/60 mb-2 flex-wrap"
								>
									<span class="bg-black/5 px-2 md:px-3 py-1 rounded-full">{exp.startDate}</span>
									<span>—</span>
									<span class="bg-black/5 px-2 md:px-3 py-1 rounded-full">{exp.endDate}</span>
								</div>

								<!-- Expandable Description -->
								{#if openJobs.has(exp.id)}
									<div
										class="mt-3 pt-3 border-t border-black/10 text-xs md:text-sm text-black/70 animate-slideDown journey-description"
									>
										{#if Array.isArray(exp.description)}
											{#each exp.description as paragraph}
												<p class="mb-3 last:mb-0">{paragraph}</p>
											{/each}
										{:else}
											<p>{exp.description}</p>
										{/if}
									</div>
								{/if}
							</div>
						</div>
					{/each}
				</div>
			</div>
		</div>

		<div class="h-12 md:h-20"></div>
	</div>
</div>

<div class="px-4 md:px-8 lg:px-12">
	<div class="mb-6 md:mb-9">
		<h2 class="text-3xl md:text-4xl font-medium whitespace-nowrap">Especialidades</h2>
	</div>

	<div class="max-w-7xl mx-auto">
		<!-- Expertise Grid -->
		<div class="grid grid-cols-1 md:grid-cols-2 gap-4 md:gap-6">
			{#each expertise as item, i}
				<div
					class="p-6 md:p-8 rounded-xl transition-all duration-300 hover:-translate-y-1 hover:shadow-xl"
					class:bg-gradient-to-br={item.colored}
					class:from-indigo-500={item.colored}
					class:to-purple-600={item.colored}
					class:text-white={item.colored}
					class:bg-gray-100={!item.colored}
					style="animation-delay: {0.4 + i * 0.1}s;"
				>
					<h4 class="text-xl md:text-2xl font-semibold mb-4">{item.title}</h4>
					<ul class="list-none p-0 m-0">
						{#each item.skills as skill}
							<li class="text-base md:text-lg py-2 pl-6 relative">
								<span class="absolute left-0 text-2xl leading-none">•</span>
								{skill}
							</li>
						{/each}
					</ul>
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

	.journey-description p {
		text-align: justify;
		text-indent: 2em;
		line-height: 1.6;
	}

	.journey-description p:first-child {
		margin-top: 0;
	}
</style>
