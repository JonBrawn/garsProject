<script lang="ts">
	import { fly, fade } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	let sectionEl: HTMLElement | undefined = $state();
	let visible = $state(false);

	const stats = [
		{ value: '35T', label: 'Army MOS', icon: 'bx-shield' },
		{ value: '3+', label: 'Skills Mastered', icon: 'bx-code-alt' },
		{ value: '6+', label: 'Projects Built', icon: 'bx-folder' },
		{ value: '∞', label: 'Passion Level', icon: 'bx-heart' }
	];

	const milestones = [
		{ year: 'Early', title: 'RPG Quest Developer', desc: 'JSON-based quests for Minecraft RPG servers', icon: 'bx-game-pad' },
		{ year: 'HS', title: 'HTML & CSS Discovery', desc: 'Fell in love with web development', icon: 'bx-code-alt' },
		{ year: 'MIL', title: 'US Army 35T', desc: 'Network intelligence specialist', icon: 'bx-shield' },
		{ year: 'POST', title: 'Trade Skills', desc: 'Precision from construction & pool tech', icon: 'bx-wrench' },
		{ year: 'NOW', title: 'Full-Time Developer', desc: 'freeCodeCamp + CS degree pursuit', icon: 'bx-rocket' }
	];

	$effect(() => {
		if (!sectionEl) return;
		const observer = new IntersectionObserver(([entry]) => {
			if (entry.isIntersecting) { visible = true; observer.disconnect(); }
		}, { threshold: 0.1 });
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section id="about" class="relative min-h-screen px-6 lg:px-10 py-24 bg-[var(--color-bg-secondary)] overflow-hidden" bind:this={sectionEl}>
	<!-- Decorative -->
	<div class="absolute top-0 left-0 w-full h-px bg-gradient-to-r from-transparent via-[var(--color-gradient-one)]/30 to-transparent"></div>
	<div class="absolute -top-32 right-[20%] w-64 h-64 bg-[var(--color-gradient-one)]/5 rounded-full blur-[100px]"></div>

	<div class="max-w-6xl mx-auto">
		{#if visible}
			<!-- Header with large number -->
			<div class="flex items-end gap-6 mb-16" in:fly={{ y: 50, duration: 700, easing: cubicOut }}>
				<span class="text-[120px] md:text-[180px] font-black leading-none text-[var(--color-text)]/[0.03] select-none">01</span>
				<div class="mb-4">
					<span class="text-xs font-bold tracking-[0.3em] uppercase text-[var(--color-gradient-one)]">About Me</span>
					<h2 class="text-4xl md:text-5xl font-black mt-1">My <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Story</span></h2>
				</div>
			</div>

			<!-- Content grid -->
			<div class="grid lg:grid-cols-[1fr_1.2fr] gap-16 mb-20">
				<!-- Left: Image + stats -->
				<div in:fly={{ x: -50, duration: 700, delay: 200, easing: cubicOut }}>
					<div class="relative mb-10">
						<div class="absolute -inset-4 bg-gradient-to-br from-[var(--color-gradient-two)]/20 to-[var(--color-gradient-one)]/20 rounded-3xl blur-xl"></div>
						<img
							src="/images/image.jpg"
							alt="Garrett Brown"
							class="relative w-full aspect-[4/5] object-cover rounded-3xl border border-white/10"
						/>
						<!-- Floating card overlay -->
						<div class="absolute -bottom-6 -right-6 px-6 py-4 rounded-2xl bg-[var(--color-bg)]/90 backdrop-blur-xl border border-white/10 shadow-2xl">
							<div class="text-3xl font-black bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">35T</div>
							<div class="text-xs text-[var(--color-text)]/50 font-medium">Army Veteran</div>
						</div>
					</div>

					<!-- Stats grid -->
					<div class="grid grid-cols-2 gap-3">
						{#each stats as stat, i}
							<div
								class="group p-4 rounded-2xl bg-white/[0.03] border border-white/5 hover:border-[var(--color-gradient-one)]/30 hover:bg-white/[0.06] transition-all duration-300 text-center"
								in:fly={{ y: 30, duration: 400, delay: 400 + i * 80, easing: cubicOut }}
							>
								<i class="bx {stat.icon} text-2xl text-[var(--color-gradient-one)]/60 group-hover:text-[var(--color-gradient-one)] transition-colors mb-1 block"></i>
								<div class="text-2xl font-black">{stat.value}</div>
								<div class="text-[10px] font-semibold uppercase tracking-wider text-[var(--color-text)]/30">{stat.label}</div>
							</div>
						{/each}
					</div>
				</div>

				<!-- Right: Text + Timeline -->
				<div>
					<p
						class="text-lg md:text-xl leading-relaxed text-[var(--color-text)]/70 font-light mb-4"
						in:fly={{ y: 30, duration: 600, delay: 300, easing: cubicOut }}
					>
						My path to web development has been anything but traditional. From writing JSON quests as a kid, to military intelligence, to finish carpentry — every experience shaped how I approach code.
					</p>
					<p
						class="text-base leading-relaxed text-[var(--color-text)]/50 mb-12"
						in:fly={{ y: 30, duration: 600, delay: 400, easing: cubicOut }}
					>
						I bring military-grade attention to detail and a construction worker's problem-solving grit to every project. Currently pursuing a CS degree while building real-world projects.
					</p>

					<!-- Horizontal timeline -->
					<div class="space-y-4">
						{#each milestones as ms, i}
							<div
								class="group flex items-start gap-4 p-4 rounded-2xl hover:bg-white/[0.04] transition-all duration-300"
								in:fly={{ x: 30, duration: 500, delay: 500 + i * 100, easing: cubicOut }}
							>
								<div class="flex-shrink-0 w-12 h-12 rounded-xl bg-gradient-to-br from-[var(--color-gradient-two)]/20 to-[var(--color-gradient-one)]/20 flex items-center justify-center group-hover:from-[var(--color-gradient-two)] group-hover:to-[var(--color-gradient-one)] group-hover:shadow-[0_0_25px_var(--color-gradient-one)]/30 transition-all duration-300">
									<i class="bx {ms.icon} text-xl text-[var(--color-gradient-one)] group-hover:text-white transition-colors"></i>
								</div>
								<div class="flex-1 min-w-0">
									<div class="flex items-center gap-3">
										<span class="text-[10px] font-black tracking-[0.2em] uppercase text-[var(--color-gradient-one)]/60">{ms.year}</span>
										<span class="flex-1 h-px bg-white/5"></span>
									</div>
									<h4 class="font-bold mt-1">{ms.title}</h4>
									<p class="text-sm text-[var(--color-text)]/40">{ms.desc}</p>
								</div>
							</div>
						{/each}
					</div>
				</div>
			</div>
		{/if}
	</div>
</section>
