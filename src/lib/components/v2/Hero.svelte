<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade, scale } from 'svelte/transition';
	import { cubicOut, elasticOut, backOut } from 'svelte/easing';
	import { base } from '$app/paths';

	let visible = $state(false);
	let mouseX = $state(0);
	let mouseY = $state(0);
	let typedLines = $state<string[]>([]);
	let currentChar = $state(0);
	let showCursor = $state(true);

	const lines = ['Web Developer.', 'Problem Solver.', 'Creative Thinker.'];
	let currentLine = 0;
	let isDeleting = false;

	const socials = [
		{ icon: 'bxl-github', href: '#', label: 'GitHub' },
		{ icon: 'bxl-linkedin-square', href: '#', label: 'LinkedIn' },
		{ icon: 'bxl-instagram-alt', href: '#', label: 'Instagram' },
		{ icon: 'bxl-twitter', href: '#', label: 'Twitter' }
	];

	// Particle system
	let particles = $state<Array<{ x: number; y: number; size: number; speed: number; opacity: number; delay: number }>>([]);

	onMount(() => {
		visible = true;

		// Generate particles
		particles = Array.from({ length: 50 }, () => ({
			x: Math.random() * 100,
			y: Math.random() * 100,
			size: Math.random() * 3 + 1,
			speed: Math.random() * 20 + 10,
			opacity: Math.random() * 0.5 + 0.1,
			delay: Math.random() * 10
		}));

		// Rotating typewriter
		let text = '';
		const type = () => {
			const fullText = lines[currentLine];
			if (!isDeleting) {
				text = fullText.slice(0, text.length + 1);
				typedLines = [text];
				if (text === fullText) {
					setTimeout(() => { isDeleting = true; type(); }, 2000);
					return;
				}
				setTimeout(type, 60 + Math.random() * 40);
			} else {
				text = text.slice(0, -1);
				typedLines = [text];
				if (text === '') {
					isDeleting = false;
					currentLine = (currentLine + 1) % lines.length;
					setTimeout(type, 500);
					return;
				}
				setTimeout(type, 30);
			}
		};
		type();

		const cursorBlink = setInterval(() => { showCursor = !showCursor; }, 530);

		// Parallax mouse
		const handleMouse = (e: MouseEvent) => {
			mouseX = (e.clientX / window.innerWidth - 0.5) * 2;
			mouseY = (e.clientY / window.innerHeight - 0.5) * 2;
		};
		window.addEventListener('mousemove', handleMouse);

		return () => {
			clearInterval(cursorBlink);
			window.removeEventListener('mousemove', handleMouse);
		};
	});
</script>

<section id="home" class="relative min-h-screen flex items-center justify-center overflow-hidden">
	<!-- Particle field -->
	<div class="absolute inset-0 pointer-events-none">
		{#each particles as p}
			<div
				class="absolute rounded-full bg-[var(--color-gradient-one)]"
				style="
					left: {p.x}%;
					width: {p.size}px;
					height: {p.size}px;
					opacity: {p.opacity};
					animation: particle-rise {p.speed}s linear infinite;
					animation-delay: -{p.delay}s;
				"
			></div>
		{/each}
	</div>

	<!-- Morphing blobs with mouse parallax -->
	<div class="absolute inset-0 pointer-events-none" style="transform: translate({mouseX * 10}px, {mouseY * 10}px)">
		<div class="absolute top-[10%] left-[15%] w-[500px] h-[500px] rounded-full bg-[var(--color-gradient-two)]/15 blur-[100px] animate-[morph_12s_ease-in-out_infinite]"></div>
		<div class="absolute bottom-[10%] right-[10%] w-[400px] h-[400px] rounded-full bg-[var(--color-gradient-one)]/15 blur-[100px] animate-[morph_12s_ease-in-out_infinite_4s]"></div>
		<div class="absolute top-[40%] right-[30%] w-[300px] h-[300px] rounded-full bg-[var(--color-accent)]/10 blur-[80px] animate-[morph_12s_ease-in-out_infinite_8s]"></div>
	</div>

	<!-- Noise texture overlay -->
	<div class="absolute inset-0 opacity-[0.015] pointer-events-none" style="background-image: url('data:image/svg+xml,%3Csvg viewBox=%270 0 256 256%27 xmlns=%27http://www.w3.org/2000/svg%27%3E%3Cfilter id=%27noise%27%3E%3CfeTurbulence type=%27fractalNoise%27 baseFrequency=%270.9%27 numOctaves=%274%27 stitchTiles=%27stitch%27/%3E%3C/filter%3E%3Crect width=%27100%25%27 height=%27100%25%27 filter=%27url(%23noise)%27/%3E%3C/svg%3E');"></div>

	<div class="relative z-10 flex flex-col items-center text-center w-full max-w-5xl px-6 lg:px-10 pt-28 pb-16">
		{#if visible}
			<!-- Photo with orbit ring -->
			<div
				class="relative mb-12"
				in:scale={{ start: 0, duration: 1000, delay: 200, easing: backOut }}
			>
				<!-- Orbit ring -->
				<div class="absolute -inset-8 rounded-full border border-[var(--color-gradient-one)]/20 animate-[spin_20s_linear_infinite]">
					<div class="absolute -top-1.5 left-1/2 w-3 h-3 rounded-full bg-[var(--color-gradient-one)] shadow-[0_0_15px_var(--color-gradient-one)]"></div>
				</div>
				<div class="absolute -inset-14 rounded-full border border-[var(--color-gradient-two)]/10 animate-[spin_30s_linear_infinite_reverse]">
					<div class="absolute top-1/2 -right-1 w-2 h-2 rounded-full bg-[var(--color-gradient-two)] shadow-[0_0_10px_var(--color-gradient-two)]"></div>
				</div>

				<div class="relative" style="transform: translate({mouseX * -5}px, {mouseY * -5}px); transition: transform 0.3s ease-out;">
					<div class="absolute -inset-1 bg-gradient-to-r from-[var(--color-gradient-two)] via-[var(--color-gradient-one)] to-[var(--color-gradient-two)] rounded-full animate-[spin_4s_linear_infinite] opacity-70 blur-[2px]"></div>
					<img
						src="{base}/images/image.jpg"
						alt="Garrett Brown"
						class="relative w-36 h-36 md:w-44 md:h-44 rounded-full object-cover border-4 border-[var(--color-bg)]"
					/>
				</div>
			</div>

			<!-- Split text reveal -->
			<div in:fly={{ y: 60, duration: 900, delay: 500, easing: cubicOut }}>
				<h1 class="text-6xl md:text-7xl lg:text-8xl xl:text-9xl font-black leading-[0.9] tracking-tighter">
					<span class="block text-[var(--color-text)]">GARRETT</span>
					<span class="block bg-gradient-to-r from-[var(--color-gradient-two)] via-[var(--color-gradient-one)] to-[var(--color-gradient-two)] bg-[length:200%_auto] bg-clip-text text-transparent animate-[gradient-shift_3s_ease_infinite]">
						BROWN
					</span>
				</h1>
			</div>

			<!-- Typewriter -->
			<div
				class="mt-6 h-10 flex items-center justify-center"
				in:fade={{ duration: 600, delay: 800 }}
			>
				<span class="text-xl md:text-2xl font-light text-[var(--color-text)]/50 tracking-wide">
					{typedLines[0] || ''}
				</span>
				<span
					class="inline-block w-[2px] h-6 bg-[var(--color-gradient-one)] ml-1 {showCursor ? 'opacity-100' : 'opacity-0'}"
				></span>
			</div>

			<!-- Bio -->
			<p
				class="mt-6 text-base md:text-lg text-[var(--color-text)]/40 max-w-xl leading-relaxed font-light"
				in:fly={{ y: 30, duration: 600, delay: 900, easing: cubicOut }}
			>
				Evolving web developer with a unique journey from military intelligence
				to crafting digital experiences. Currently leveling up through freeCodeCamp
				and pursuing a CS degree.
			</p>

			<!-- Social row -->
			<div
				class="flex items-center gap-6 mt-10"
				in:fly={{ y: 20, duration: 500, delay: 1000, easing: cubicOut }}
			>
				{#each socials as social, i}
					<a
						href={social.href}
						class="group relative w-12 h-12 flex items-center justify-center text-[var(--color-text)]/30 text-xl hover:text-[var(--color-gradient-one)] transition-all duration-300"
						aria-label={social.label}
						in:scale={{ start: 0, duration: 500, delay: 1100 + i * 80, easing: elasticOut }}
					>
						<i class="bx {social.icon} relative z-10"></i>
						<!-- Hover ring -->
						<span class="absolute inset-0 rounded-full border border-transparent group-hover:border-[var(--color-gradient-one)]/30 group-hover:shadow-[0_0_20px_var(--color-gradient-one)]/20 scale-0 group-hover:scale-100 transition-all duration-300"></span>
					</a>
				{/each}

				<div class="w-px h-6 bg-[var(--color-text)]/10"></div>

				<a
					href="#about"
					class="group flex items-center gap-2 text-xs font-bold uppercase tracking-[0.2em] text-[var(--color-text)]/30 hover:text-[var(--color-gradient-one)] transition-colors duration-300"
					in:fly={{ x: 20, duration: 400, delay: 1300, easing: cubicOut }}
				>
					Explore
					<i class="bx bx-chevron-down text-base animate-bounce"></i>
				</a>
			</div>

			<!-- Scroll line -->
			<div
				class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-3"
				in:fade={{ duration: 800, delay: 1500 }}
			>
				<div class="w-px h-16 bg-gradient-to-b from-transparent to-[var(--color-gradient-one)]/30 animate-[scroll-line_2s_ease-in-out_infinite]"></div>
			</div>
		{/if}
	</div>
</section>
