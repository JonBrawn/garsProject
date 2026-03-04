<script lang="ts">
	import { fly, scale } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	interface Skill {
		icon: string;
		title: string;
		description: string;
	}

	interface Props {
		id: string;
		sectionNum: string;
		label: string;
		title: string;
		titleAccent: string;
		skills: Skill[];
	}

	let { id, sectionNum, label, title, titleAccent, skills }: Props = $props();

	let sectionEl: HTMLElement | undefined = $state();
	let visible = $state(false);
	let hoveredIdx = $state(-1);

	$effect(() => {
		if (!sectionEl) return;
		const observer = new IntersectionObserver(([entry]) => {
			if (entry.isIntersecting) { visible = true; observer.disconnect(); }
		}, { threshold: 0.1 });
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section {id} class="relative min-h-screen px-6 lg:px-10 py-24 bg-[var(--color-bg)] overflow-hidden" bind:this={sectionEl}>
	<div class="absolute top-0 left-0 w-full h-px bg-gradient-to-r from-transparent via-[var(--color-gradient-two)]/20 to-transparent"></div>

	<div class="max-w-6xl mx-auto">
		{#if visible}
			<!-- Header -->
			<div class="flex items-end gap-6 mb-16" in:fly={{ y: 50, duration: 700, easing: cubicOut }}>
				<span class="text-[120px] md:text-[180px] font-black leading-none text-[var(--color-text)]/[0.03] select-none">{sectionNum}</span>
				<div class="mb-4">
					<span class="text-xs font-bold tracking-[0.3em] uppercase text-[var(--color-gradient-one)]">{label}</span>
					<h2 class="text-4xl md:text-5xl font-black mt-1">{title} <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">{titleAccent}</span></h2>
				</div>
			</div>

			<!-- Cards with neon borders -->
			<div class="grid grid-cols-1 md:grid-cols-3 gap-6">
				{#each skills as skill, i}
					<div
						class="group relative cursor-default"
						in:fly={{ y: 80, duration: 600, delay: i * 150, easing: cubicOut }}
						onmouseenter={() => (hoveredIdx = i)}
						onmouseleave={() => (hoveredIdx = -1)}
					>
						<!-- Neon border glow -->
						<div class="absolute -inset-px rounded-3xl bg-gradient-to-br from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] opacity-0 group-hover:opacity-100 transition-opacity duration-500 blur-[1px]"></div>

						<!-- Card body -->
						<div class="relative h-full p-8 rounded-3xl bg-[var(--color-bg)] border border-white/5 group-hover:border-transparent transition-all duration-500 overflow-hidden">
							<!-- Spotlight effect -->
							<div class="absolute inset-0 bg-gradient-to-br from-[var(--color-gradient-one)]/0 to-[var(--color-gradient-two)]/0 group-hover:from-[var(--color-gradient-one)]/5 group-hover:to-[var(--color-gradient-two)]/10 transition-all duration-700"></div>

							<!-- Corner decoration -->
							<div class="absolute top-0 right-0 w-20 h-20">
								<div class="absolute top-3 right-3 w-full h-full border-t-2 border-r-2 border-[var(--color-gradient-one)]/0 group-hover:border-[var(--color-gradient-one)]/30 rounded-tr-2xl transition-all duration-500 group-hover:w-12 group-hover:h-12"></div>
							</div>

							<div class="relative z-10">
								<!-- Large icon -->
								<div class="w-20 h-20 rounded-2xl bg-gradient-to-br from-[var(--color-gradient-two)]/10 to-[var(--color-gradient-one)]/10 flex items-center justify-center mb-6 group-hover:shadow-[0_0_40px_var(--color-gradient-one)]/20 transition-all duration-500">
									<i class="bx {skill.icon} text-4xl text-[var(--color-gradient-one)]/70 group-hover:text-[var(--color-gradient-one)] group-hover:scale-110 transition-all duration-300"></i>
								</div>

								<h4 class="text-xl font-bold mb-3 group-hover:text-[var(--color-gradient-one)] transition-colors duration-300">{skill.title}</h4>
								<p class="text-sm text-[var(--color-text)]/40 leading-relaxed group-hover:text-[var(--color-text)]/60 transition-colors duration-300">{skill.description}</p>

								<!-- Bottom accent line -->
								<div class="mt-6 h-[2px] rounded-full bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] scale-x-0 group-hover:scale-x-100 origin-left transition-transform duration-500"></div>
							</div>
						</div>
					</div>
				{/each}
			</div>
		{/if}
	</div>
</section>
