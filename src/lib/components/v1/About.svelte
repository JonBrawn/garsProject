<script lang="ts">
	import { fly, fade, scale } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	let sectionEl: HTMLElement | undefined = $state();
	let visible = $state(false);

	const timeline = [
		{
			icon: 'bx-game-pad',
			period: 'Early Years',
			title: 'Minecraft RPG Lore Team',
			description: 'First foray into programming — writing JSON quests for an RPG Minecraft server. Sparked a lifelong passion for code.'
		},
		{
			icon: 'bx-code-alt',
			period: 'High School',
			title: 'HTML & CSS Foundations',
			description: 'Took a web development class covering the basics of HTML and CSS. Fell in love with building for the web.'
		},
		{
			icon: 'bx-shield',
			period: 'Military Service',
			title: 'US Army — 35T',
			description: 'Served as a Military Intelligence Systems Maintainer/Integrator. The network specialist for the intelligence community.'
		},
		{
			icon: 'bx-wrench',
			period: 'Post-Service',
			title: 'Construction & Trades',
			description: 'Refined attention to detail in finish construction and pool maintenance — skills that translate directly to clean, precise code.'
		},
		{
			icon: 'bx-rocket',
			period: 'Present',
			title: 'Web Development Journey',
			description: 'Studying through freeCodeCamp and pursuing a Bachelor\'s in Computer Science. Building the future one project at a time.'
		}
	];

	$effect(() => {
		if (!sectionEl) return;
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) {
					visible = true;
					observer.disconnect();
				}
			},
			{ threshold: 0.1 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	id="about"
	class="relative min-h-screen px-6 lg:px-10 py-24 bg-[var(--color-bg-secondary)] overflow-hidden"
	bind:this={sectionEl}
>
	<!-- Subtle bg glow -->
	<div class="absolute top-0 right-0 w-96 h-96 bg-[var(--color-gradient-two)]/10 rounded-full blur-[150px] pointer-events-none"></div>

	<div class="max-w-6xl mx-auto">
		{#if visible}
			<!-- Section header -->
			<div class="text-center mb-16" in:fly={{ y: 40, duration: 600, easing: cubicOut }}>
				<span class="inline-block text-xs font-semibold tracking-[0.2em] uppercase text-[var(--color-gradient-one)] mb-3">Get to know me</span>
				<h2 class="text-4xl md:text-5xl lg:text-6xl font-bold">
					My <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Journey</span>
				</h2>
			</div>

			<!-- Intro text + image -->
			<div
				class="flex flex-col lg:flex-row items-center gap-12 mb-20"
				in:fly={{ y: 40, duration: 600, delay: 150, easing: cubicOut }}
			>
				<div class="relative group flex-shrink-0">
					<div class="absolute -inset-2 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] rounded-2xl blur opacity-30 group-hover:opacity-50 transition-opacity duration-500"></div>
					<img
						src="/images/image.jpg"
						alt="Garrett Brown"
						class="relative w-48 h-48 md:w-56 md:h-56 rounded-2xl object-cover border border-white/10"
					/>
				</div>
				<div class="flex-1 text-center lg:text-left">
					<p class="text-base md:text-lg leading-relaxed text-[var(--color-text)]/80">
						From crafting RPG quests as a kid to serving in military intelligence, my path to web development has been anything but traditional. Each experience sharpened my problem-solving instincts and attention to detail — skills I now channel into building beautiful, functional websites.
					</p>
					<p class="text-base md:text-lg leading-relaxed text-[var(--color-text)]/80 mt-4">
						I believe the best developers are lifelong learners, and I'm committed to growing every day.
					</p>
				</div>
			</div>

			<!-- Timeline -->
			<div class="relative">
				<!-- Timeline line -->
				<div class="absolute left-6 md:left-1/2 top-0 bottom-0 w-px bg-gradient-to-b from-[var(--color-gradient-two)] via-[var(--color-gradient-one)] to-[var(--color-gradient-two)] md:-translate-x-px"></div>

				<div class="flex flex-col gap-12">
					{#each timeline as item, i}
						<div
							class="relative flex flex-col md:flex-row items-start gap-6 {i % 2 === 0 ? 'md:flex-row' : 'md:flex-row-reverse'}"
							in:fly={{ y: 40, duration: 500, delay: 300 + i * 120, easing: cubicOut }}
						>
							<!-- Dot -->
							<div class="absolute left-6 md:left-1/2 w-3 h-3 rounded-full bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] -translate-x-1.5 mt-6 shadow-[0_0_15px_var(--color-accent)] z-10"></div>

							<!-- Spacer for mobile -->
							<div class="hidden md:block md:w-1/2"></div>

							<!-- Card -->
							<div class="ml-14 md:ml-0 md:w-1/2 {i % 2 === 0 ? 'md:pr-12' : 'md:pl-12'}">
								<div class="group p-6 rounded-2xl bg-white/5 border border-white/10 backdrop-blur-sm hover:bg-white/10 hover:border-[var(--color-accent)]/30 transition-all duration-300 hover:shadow-[0_0_30px_var(--color-accent)]/10">
									<div class="flex items-center gap-3 mb-3">
										<div class="w-10 h-10 rounded-xl bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] flex items-center justify-center">
											<i class="bx {item.icon} text-xl text-white"></i>
										</div>
										<span class="text-xs font-semibold tracking-wider uppercase text-[var(--color-gradient-one)]">{item.period}</span>
									</div>
									<h3 class="text-lg font-bold mb-2">{item.title}</h3>
									<p class="text-sm text-[var(--color-text)]/60 leading-relaxed">{item.description}</p>
								</div>
							</div>
						</div>
					{/each}
				</div>
			</div>
		{/if}
	</div>
</section>
