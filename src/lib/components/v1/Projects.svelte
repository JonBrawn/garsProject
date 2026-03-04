<script lang="ts">
	import { fly } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	const projects = [
		{ title: 'Project 1', image: '/images/project1.png', tag: 'Web App' },
		{ title: 'Project 2', image: '/images/project2.png', tag: 'Design' },
		{ title: 'Project 3', image: '/images/project3.png', tag: 'Frontend' },
		{ title: 'Project 4', image: '/images/project4.png', tag: 'Full Stack' },
		{ title: 'Project 5', image: '/images/project5.png', tag: 'UI/UX' },
		{ title: 'Project 6', image: '/images/project6.png', tag: 'Concept' }
	];

	const placeholderDesc = 'A showcase project demonstrating modern web development techniques, responsive design, and clean user interfaces.';

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
			{ threshold: 0.05 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	id="projects"
	class="relative min-h-screen px-6 lg:px-10 py-24 bg-[var(--color-bg-secondary)] overflow-hidden"
	bind:this={sectionEl}
>
	<div class="absolute top-1/2 right-0 w-96 h-96 bg-[var(--color-gradient-one)]/10 rounded-full blur-[150px] pointer-events-none"></div>

	<div class="max-w-6xl mx-auto">
		{#if visible}
			<div class="text-center mb-16" in:fly={{ y: 40, duration: 600, easing: cubicOut }}>
				<span class="inline-block text-xs font-semibold tracking-[0.2em] uppercase text-[var(--color-gradient-one)] mb-3">Portfolio</span>
				<h2 class="text-4xl md:text-5xl lg:text-6xl font-bold">
					Featured <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Projects</span>
				</h2>
			</div>

			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
				{#each projects as project, i}
					<div
						class="group relative rounded-2xl overflow-hidden bg-white/5 border border-white/10 backdrop-blur-sm hover:border-[var(--color-accent)]/30 transition-all duration-500 hover:shadow-[0_0_40px_var(--color-accent)]/10 hover:-translate-y-2 cursor-pointer"
						in:fly={{ y: 50, duration: 500, delay: i * 100, easing: cubicOut }}
					>
						<!-- Image -->
						<div class="relative aspect-video overflow-hidden bg-[var(--color-box)]">
							<img
								src={project.image}
								alt={project.title}
								class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-700"
							/>
							<div class="absolute inset-0 bg-gradient-to-t from-[var(--color-bg)] via-transparent to-transparent opacity-60"></div>

							<!-- Tag -->
							<div class="absolute top-4 left-4 px-3 py-1 rounded-full bg-[var(--color-bg)]/70 backdrop-blur-md border border-white/10 text-xs font-medium">
								{project.tag}
							</div>
						</div>

						<!-- Content -->
						<div class="p-6">
							<h3 class="text-lg font-bold mb-2 group-hover:text-[var(--color-gradient-one)] transition-colors duration-300">{project.title}</h3>
							<p class="text-sm text-[var(--color-text)]/60 leading-relaxed mb-5">{placeholderDesc}</p>

							<div class="flex items-center gap-3">
								<span class="inline-flex items-center gap-2 text-sm font-semibold text-[var(--color-gradient-one)] group-hover:gap-3 transition-all duration-300">
									View Project <i class="bx bx-right-arrow-alt text-lg"></i>
								</span>
							</div>
						</div>

						<!-- Hover overlay glow -->
						<div class="absolute inset-0 bg-gradient-to-br from-[var(--color-gradient-two)]/0 to-[var(--color-gradient-one)]/0 group-hover:from-[var(--color-gradient-two)]/5 group-hover:to-[var(--color-gradient-one)]/5 transition-all duration-500 pointer-events-none"></div>
					</div>
				{/each}
			</div>
		{/if}
	</div>
</section>
