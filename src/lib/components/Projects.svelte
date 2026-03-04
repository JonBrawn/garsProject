<script lang="ts">
	import { fly, scale } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	const projects = [
		{ title: 'Project 1', image: 'images/project1.png' },
		{ title: 'Project 2', image: 'images/project2.png' },
		{ title: 'Project 3', image: 'images/project3.png' },
		{ title: 'Project 4', image: 'images/project4.png' },
		{ title: 'Project 5', image: 'images/project5.png' },
		{ title: 'Project 6', image: 'images/project6.png' }
	];

	const placeholderDesc =
		'Lorem ipsum dolor sit amet consectetur adipisicing elit. Iure reprehenderit officiis pariatur dolore perferendis veritatis quibusdam amet minus esse perspiciatis veniam eveniet nesciunt aut, nostrum odio corrupti.';

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
			{ threshold: 0.1 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	id="projects"
	class="min-h-screen px-[8%] lg:px-[15%] py-20 bg-[var(--color-bg-secondary)]"
	bind:this={sectionEl}
>
	{#if visible}
		<h2
			class="text-center text-4xl md:text-5xl lg:text-6xl font-bold mb-14"
			in:fly={{ y: 40, duration: 600, easing: cubicOut }}
		>
			<span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Projects</span>
		</h2>

		<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 max-w-6xl mx-auto">
			{#each projects as project, i}
				<div
					class="group flex flex-col items-center text-center bg-[var(--color-box)] border-2 border-[var(--color-accent)] rounded-3xl p-8 gap-5 cursor-pointer shadow-[0_0_5px_var(--color-accent)] hover:shadow-[0_0_25px_var(--color-accent),0_0_50px_var(--color-accent)] hover:scale-[1.02] transition-all duration-300 overflow-hidden"
					in:fly={{ y: 50, duration: 500, delay: i * 100, easing: cubicOut }}
				>
					<div class="overflow-hidden rounded-2xl">
						<img
							src={project.image}
							alt={project.title}
							class="max-w-[280px] w-full rounded-2xl group-hover:scale-110 transition-transform duration-500"
						/>
					</div>
					<h3 class="text-2xl font-bold text-[var(--color-text)]">{project.title}</h3>
					<p class="text-sm text-[var(--color-text)] opacity-80 leading-relaxed">{placeholderDesc}</p>
					<div
						class="inline-block px-7 py-2.5 bg-[var(--color-accent)] text-[var(--color-btn-text)] rounded-full text-base font-semibold shadow-[0_0_20px_var(--color-accent)] hover:scale-105 hover:shadow-[0_0_25px_var(--color-accent),0_0_50px_var(--color-accent)] transition-all duration-300 mt-auto"
					>
						Review Project
					</div>
				</div>
			{/each}
		</div>
	{/if}
</section>
