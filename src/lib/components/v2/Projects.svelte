<script lang="ts">
	import { fly, fade } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';
	import { base } from '$app/paths';

	const projects = [
		{ title: 'Project 1', image: 'images/project1.png', tag: 'WEB', desc: 'Modern web application with responsive design and clean architecture.' },
		{ title: 'Project 2', image: 'images/project2.png', tag: 'UI', desc: 'User interface design focusing on accessibility and visual polish.' },
		{ title: 'Project 3', image: 'images/project3.png', tag: 'DEV', desc: 'Frontend development with modern frameworks and best practices.' },
		{ title: 'Project 4', image: 'images/project4.png', tag: 'APP', desc: 'Full-stack application demonstrating end-to-end development.' },
		{ title: 'Project 5', image: 'images/project5.png', tag: 'UX', desc: 'User experience design with research-driven approach.' },
		{ title: 'Project 6', image: 'images/project6.png', tag: 'ART', desc: 'Creative concept exploring the intersection of design and code.' }
	];

	let sectionEl: HTMLElement | undefined = $state();
	let visible = $state(false);

	$effect(() => {
		if (!sectionEl) return;
		const observer = new IntersectionObserver(([entry]) => {
			if (entry.isIntersecting) { visible = true; observer.disconnect(); }
		}, { threshold: 0.05 });
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section id="projects" class="relative min-h-screen px-6 lg:px-10 py-24 bg-[var(--color-bg-secondary)] overflow-hidden" bind:this={sectionEl}>
	<div class="absolute top-0 left-0 w-full h-px bg-gradient-to-r from-transparent via-[var(--color-gradient-one)]/20 to-transparent"></div>
	<div class="absolute bottom-[20%] left-0 w-96 h-96 bg-[var(--color-gradient-two)]/5 rounded-full blur-[120px]"></div>

	<div class="max-w-6xl mx-auto">
		{#if visible}
			<!-- Header -->
			<div class="flex items-end gap-6 mb-16" in:fly={{ y: 50, duration: 700, easing: cubicOut }}>
				<span class="text-[120px] md:text-[180px] font-black leading-none text-[var(--color-text)]/[0.03] select-none">04</span>
				<div class="mb-4">
					<span class="text-xs font-bold tracking-[0.3em] uppercase text-[var(--color-gradient-one)]">Portfolio</span>
					<h2 class="text-4xl md:text-5xl font-black mt-1">Featured <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Work</span></h2>
				</div>
			</div>

			<!-- Bento grid -->
			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
				{#each projects as project, i}
					{@const isLarge = i === 0 || i === 3}
					<div
						class="group relative overflow-hidden rounded-3xl cursor-pointer
							{isLarge ? 'md:col-span-2 md:row-span-1' : ''}
							{isLarge ? 'aspect-[2/1]' : 'aspect-square'}"
						in:fly={{ y: 60, duration: 500, delay: i * 100, easing: cubicOut }}
					>
						<!-- Image -->
						<div class="absolute inset-0 bg-[var(--color-box)]">
							<img
								src="{base}/{project.image}"
								alt={project.title}
								class="w-full h-full object-cover opacity-60 group-hover:opacity-30 group-hover:scale-110 transition-all duration-700"
							/>
						</div>

						<!-- Gradient overlay -->
						<div class="absolute inset-0 bg-gradient-to-t from-[var(--color-bg)] via-[var(--color-bg)]/50 to-transparent opacity-70 group-hover:opacity-90 transition-opacity duration-500"></div>

						<!-- Neon border on hover -->
						<div class="absolute inset-0 rounded-3xl border border-white/5 group-hover:border-[var(--color-gradient-one)]/30 group-hover:shadow-[inset_0_0_30px_var(--color-gradient-one)]/5 transition-all duration-500"></div>

						<!-- Content -->
						<div class="absolute inset-0 p-6 flex flex-col justify-end z-10">
							<!-- Tag -->
							<span class="self-start mb-auto px-3 py-1 text-[10px] font-black tracking-[0.2em] uppercase text-[var(--color-gradient-one)] border border-[var(--color-gradient-one)]/30 rounded-full backdrop-blur-md">
								{project.tag}
							</span>

							<div class="transform translate-y-4 group-hover:translate-y-0 transition-transform duration-500">
								<h3 class="text-2xl font-black mb-2">{project.title}</h3>
								<p class="text-sm text-[var(--color-text)]/40 opacity-0 group-hover:opacity-100 transition-opacity duration-500 delay-100 max-w-sm">{project.desc}</p>

								<div class="flex items-center gap-2 mt-4 opacity-0 group-hover:opacity-100 transition-all duration-500 delay-200">
									<span class="text-xs font-bold uppercase tracking-[0.15em] text-[var(--color-gradient-one)]">View Project</span>
									<div class="w-6 h-px bg-[var(--color-gradient-one)] group-hover:w-10 transition-all duration-300"></div>
									<i class="bx bx-right-arrow-alt text-[var(--color-gradient-one)]"></i>
								</div>
							</div>
						</div>
					</div>
				{/each}
			</div>
		{/if}
	</div>
</section>
