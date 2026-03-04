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
		title: string;
		titleAccent: string;
		skills: Skill[];
		alternate?: boolean;
	}

	let { id, title, titleAccent, skills, alternate = false }: Props = $props();

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
	class="min-h-screen px-[8%] lg:px-[15%] py-20 {alternate ? 'bg-[var(--color-bg-secondary)]' : 'bg-[var(--color-bg)]'}"
	bind:this={sectionEl}
>
	{#if visible}
		<h2
			class="text-center text-4xl md:text-5xl lg:text-6xl font-bold mb-14"
			in:fly={{ y: 40, duration: 600, easing: cubicOut }}
		>
			{title} <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">{titleAccent}</span>
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-6xl mx-auto">
			{#each skills as skill, i}
				<div
					class="group relative flex flex-col items-center justify-center text-center p-10 rounded-3xl bg-[var(--color-accent)] border-4 border-transparent cursor-pointer transition-all duration-400 hover:bg-[var(--color-bg-tertiary)] hover:border-[var(--color-accent)] hover:scale-[1.03] min-h-[350px] overflow-hidden"
					in:fly={{ y: 60, duration: 500, delay: i * 120, easing: cubicOut }}
				>
					<div class="absolute inset-0 bg-gradient-to-br from-white/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 rounded-3xl"></div>
					<i class="bx {skill.icon} text-7xl mb-4 transition-transform duration-300 group-hover:scale-110 relative z-10"></i>
					<h4 class="text-2xl md:text-3xl font-extrabold mb-4 relative z-10">{skill.title}</h4>
					<p class="text-sm font-semibold leading-relaxed opacity-90 relative z-10">{skill.description}</p>
				</div>
			{/each}
		</div>
	{/if}
</section>
