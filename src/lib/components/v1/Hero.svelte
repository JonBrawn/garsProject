<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade, scale } from 'svelte/transition';
	import { cubicOut, elasticOut } from 'svelte/easing';
	import { base } from '$app/paths';

	let visible = $state(false);
	let typedText = $state('');
	let showCursor = $state(true);

	const fullTitle = 'Web Developer';
	const socials = [
		{ icon: 'bxl-github', href: '#', label: 'GitHub' },
		{ icon: 'bxl-linkedin-square', href: '#', label: 'LinkedIn' },
		{ icon: 'bxl-instagram-alt', href: '#', label: 'Instagram' },
		{ icon: 'bxl-twitter', href: '#', label: 'Twitter' }
	];

	onMount(() => {
		visible = true;

		// Typewriter effect
		let i = 0;
		const typeInterval = setInterval(() => {
			if (i < fullTitle.length) {
				typedText = fullTitle.slice(0, i + 1);
				i++;
			} else {
				clearInterval(typeInterval);
			}
		}, 80);

		// Cursor blink
		const cursorInterval = setInterval(() => {
			showCursor = !showCursor;
		}, 530);

		return () => {
			clearInterval(typeInterval);
			clearInterval(cursorInterval);
		};
	});
</script>

<section id="home" class="relative min-h-screen flex items-center justify-center overflow-hidden">
	<!-- Animated gradient blobs -->
	<div class="absolute inset-0 overflow-hidden pointer-events-none">
		<div class="absolute -top-40 -left-40 w-96 h-96 bg-[var(--color-gradient-one)]/20 rounded-full blur-[120px] animate-[blob_8s_ease-in-out_infinite]"></div>
		<div class="absolute -bottom-40 -right-40 w-96 h-96 bg-[var(--color-gradient-two)]/20 rounded-full blur-[120px] animate-[blob_8s_ease-in-out_infinite_2s]"></div>
		<div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[600px] h-[600px] bg-[var(--color-accent)]/10 rounded-full blur-[150px] animate-[blob_10s_ease-in-out_infinite_4s]"></div>
	</div>

	<!-- Grid overlay -->
	<div class="absolute inset-0 opacity-[0.03]" style="background-image: linear-gradient(var(--color-text) 1px, transparent 1px), linear-gradient(90deg, var(--color-text) 1px, transparent 1px); background-size: 60px 60px;"></div>

	<div class="relative z-10 flex flex-col-reverse lg:flex-row items-center justify-center gap-16 lg:gap-24 w-full max-w-7xl px-6 lg:px-10 pt-28 pb-16">
		<!-- Text -->
		<div class="flex flex-col items-center lg:items-start text-center lg:text-left flex-1 max-w-2xl">
			{#if visible}
				<!-- Badge -->
				<div
					class="inline-flex items-center gap-2 px-4 py-1.5 rounded-full bg-white/5 border border-white/10 backdrop-blur-sm mb-6"
					in:fly={{ y: 30, duration: 600, easing: cubicOut }}
				>
					<span class="w-2 h-2 rounded-full bg-[var(--color-hover)] animate-pulse"></span>
					<span class="text-xs font-medium text-[var(--color-text)]/70">Available for opportunities</span>
				</div>

				<h1
					class="text-5xl md:text-6xl lg:text-7xl xl:text-8xl font-extrabold leading-[1.05] tracking-tight"
					in:fly={{ y: 50, duration: 800, easing: cubicOut }}
				>
					Hi, I'm
					<br />
					<span class="bg-gradient-to-r from-[var(--color-gradient-two)] via-[var(--color-gradient-one)] to-[var(--color-gradient-two)] bg-[length:200%_auto] bg-clip-text text-transparent animate-[gradient-shift_4s_ease_infinite]">
						Garrett
					</span>
				</h1>

				<div
					class="mt-4 text-xl md:text-2xl lg:text-3xl font-medium text-[var(--color-text)]/60"
					in:fly={{ y: 40, duration: 700, delay: 200, easing: cubicOut }}
				>
					<span>{typedText}</span><span class="inline-block w-0.5 h-7 bg-[var(--color-gradient-one)] ml-1 align-middle {showCursor ? 'opacity-100' : 'opacity-0'} transition-opacity duration-100"></span>
				</div>

				<p
					class="text-base md:text-lg leading-relaxed mt-6 text-[var(--color-text)]/70 max-w-lg"
					in:fly={{ y: 40, duration: 700, delay: 400, easing: cubicOut }}
				>
					Crafting digital experiences with clean code and creative vision.
					Currently leveling up through freeCodeCamp and pursuing a CS degree.
				</p>

				<!-- Social + CTA row -->
				<div
					class="flex flex-wrap items-center gap-4 mt-10"
					in:fly={{ y: 30, duration: 600, delay: 600, easing: cubicOut }}
				>
					<a
						href="#about"
						class="group inline-flex items-center gap-2 px-7 py-3.5 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] text-[var(--color-btn-text)] rounded-full text-base font-semibold shadow-[0_0_30px_var(--color-accent)]/50 hover:shadow-[0_0_50px_var(--color-accent)] hover:scale-105 transition-all duration-300"
					>
						Explore My Work
						<i class="bx bx-right-arrow-alt text-xl group-hover:translate-x-1 transition-transform"></i>
					</a>

					<div class="flex gap-2">
						{#each socials as social, i}
							<a
								href={social.href}
								class="w-11 h-11 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-[var(--color-text)]/60 text-lg hover:bg-[var(--color-accent)] hover:text-[var(--color-btn-text)] hover:border-[var(--color-accent)] hover:scale-110 hover:-translate-y-1 hover:shadow-[0_0_25px_var(--color-accent)]/50 transition-all duration-300"
								aria-label={social.label}
								in:scale={{ start: 0, duration: 500, delay: 700 + i * 80, easing: elasticOut }}
							>
								<i class="bx {social.icon}"></i>
							</a>
						{/each}
					</div>
				</div>

				<!-- Scroll indicator -->
				<div
					class="hidden lg:flex flex-col items-center gap-2 mt-16 opacity-40"
					in:fade={{ duration: 800, delay: 1200 }}
				>
					<span class="text-xs tracking-widest uppercase">Scroll</span>
					<div class="w-5 h-8 rounded-full border-2 border-[var(--color-text)]/30 flex justify-center pt-1.5">
						<div class="w-1 h-2 rounded-full bg-[var(--color-text)]/50 animate-[scroll-dot_2s_ease-in-out_infinite]"></div>
					</div>
				</div>
			{/if}
		</div>

		<!-- Image -->
		<div class="flex-shrink-0">
			{#if visible}
				<div in:scale={{ start: 0.7, duration: 900, delay: 300, easing: cubicOut }}>
					<div class="relative group">
						<!-- Rotating gradient ring -->
						<div class="absolute -inset-3 rounded-full bg-gradient-to-r from-[var(--color-gradient-two)] via-[var(--color-gradient-one)] to-[var(--color-gradient-two)] opacity-60 blur-sm group-hover:opacity-90 transition-opacity duration-700 animate-[spin_8s_linear_infinite]"></div>
						<div class="absolute -inset-3 rounded-full bg-[var(--color-bg)] opacity-90"></div>

						<!-- Glow -->
						<div class="absolute -inset-6 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] rounded-full blur-2xl opacity-20 group-hover:opacity-40 transition-opacity duration-700"></div>

						<img
							src="{base}/images/image.jpg"
							alt="Garrett Brown"
							class="relative w-56 h-56 md:w-72 md:h-72 lg:w-80 lg:h-80 rounded-full object-cover border-2 border-white/10 shadow-2xl group-hover:scale-[1.02] transition-transform duration-500"
						/>

						<!-- Floating badges -->
						<div class="absolute -right-4 top-8 px-3 py-1.5 rounded-full bg-[var(--color-bg)]/80 backdrop-blur-md border border-white/10 text-xs font-medium animate-[float_4s_ease-in-out_infinite] shadow-lg">
							<i class="bx bxl-html5 text-orange-400 mr-1"></i> HTML5
						</div>
						<div class="absolute -left-4 bottom-12 px-3 py-1.5 rounded-full bg-[var(--color-bg)]/80 backdrop-blur-md border border-white/10 text-xs font-medium animate-[float_4s_ease-in-out_infinite_1s] shadow-lg">
							<i class="bx bxl-css3 text-blue-400 mr-1"></i> CSS3
						</div>
						<div class="absolute -right-2 bottom-4 px-3 py-1.5 rounded-full bg-[var(--color-bg)]/80 backdrop-blur-md border border-white/10 text-xs font-medium animate-[float_4s_ease-in-out_infinite_2s] shadow-lg">
							<i class="bx bxl-figma text-pink-400 mr-1"></i> Design
						</div>
					</div>
				</div>
			{/if}
		</div>
	</div>
</section>
