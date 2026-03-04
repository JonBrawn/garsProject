<script lang="ts">
	import { fly, scale } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	interface Skill {
		icon: string;
		title: string;
		description: string;
		color: string;
	}

	interface Props {
		id: string;
		label: string;
		title: string;
		titleAccent: string;
		skills: Skill[];
		alternate?: boolean;
	}

	let { id, label, title, titleAccent, skills, alternate = false }: Props = $props();

	let sectionEl: HTMLElement | undefined = $state();
	let visible = $state(false);

	$effect(() => {
		if (!sectionEl) return;
		const observer = new IntersectionObserver(
			([entry]) => {
				if (entry.isIntersecting) {
					visible = true;
					observer.disconnect();
				}
			},
			{ threshold: 0.15 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	{id}
	class="relative min-h-screen px-6 lg:px-10 py-24 overflow-hidden {alternate ? 'bg-[var(--color-bg-secondary)]' : 'bg-[var(--color-bg)]'}"
	bind:this={sectionEl}
>
	<!-- Bg glow -->
	<div class="absolute bottom-0 left-0 w-80 h-80 bg-[var(--color-gradient-one)]/10 rounded-full blur-[120px] pointer-events-none"></div>

	<div class="max-w-6xl mx-auto">
		{#if visible}
			<!-- Section header -->
			<div class="text-center mb-16" in:fly={{ y: 40, duration: 600, easing: cubicOut }}>
				<span class="inline-block text-xs font-semibold tracking-[0.2em] uppercase text-[var(--color-gradient-one)] mb-3">{label}</span>
				<h2 class="text-4xl md:text-5xl lg:text-6xl font-bold">
					{title} <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">{titleAccent}</span>
				</h2>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
				{#each skills as skill, i}
					<div
						class="group relative p-8 rounded-2xl bg-white/5 border border-white/10 backdrop-blur-sm hover:bg-white/[0.08] hover:border-[var(--color-accent)]/30 transition-all duration-500 hover:shadow-[0_0_40px_var(--color-accent)]/10 hover:-translate-y-2 cursor-default overflow-hidden"
						in:fly={{ y: 60, duration: 500, delay: i * 120, easing: cubicOut }}
					>
						<!-- Hover gradient overlay -->
						<div class="absolute inset-0 bg-gradient-to-br from-[var(--color-gradient-two)]/0 to-[var(--color-gradient-one)]/0 group-hover:from-[var(--color-gradient-two)]/5 group-hover:to-[var(--color-gradient-one)]/5 transition-all duration-500 rounded-2xl"></div>

						<!-- Icon -->
						<div class="relative z-10 w-16 h-16 rounded-2xl bg-gradient-to-br from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] flex items-center justify-center mb-6 group-hover:scale-110 group-hover:shadow-[0_0_30px_var(--color-accent)]/30 transition-all duration-300">
							<i class="bx {skill.icon} text-3xl text-white"></i>
						</div>

						<!-- Content -->
						<h4 class="relative z-10 text-xl font-bold mb-3">{skill.title}</h4>
						<p class="relative z-10 text-sm text-[var(--color-text)]/60 leading-relaxed">{skill.description}</p>

						<!-- Corner accent -->
						<div class="absolute -bottom-4 -right-4 w-24 h-24 bg-gradient-to-br from-[var(--color-gradient-two)]/10 to-transparent rounded-full blur-xl opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
					</div>
				{/each}
			</div>
		{/if}
	</div>
</section>
