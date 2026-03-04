<script lang="ts">
	import { fly, scale } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';
	import { base } from '$app/paths';

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
			{ threshold: 0.2 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	id="about"
	class="min-h-screen flex items-center justify-center px-[8%] lg:px-[15%] py-20 bg-[var(--color-bg-secondary)]"
	bind:this={sectionEl}
>
	<div class="flex flex-col-reverse lg:flex-row items-center justify-center gap-12 lg:gap-20 w-full max-w-6xl">
		<!-- Image -->
		{#if visible}
			<div in:scale={{ start: 0.8, duration: 700, easing: cubicOut }}>
				<div class="relative group">
					<div class="absolute -inset-1 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] rounded-full blur-md opacity-40 group-hover:opacity-70 transition-opacity duration-500"></div>
					<img
						src="{base}/images/image.jpg"
						alt="Garrett Brown"
						class="relative w-52 h-52 md:w-72 md:h-72 lg:w-80 lg:h-80 rounded-full object-cover shadow-[0_0_25px_var(--color-accent)] group-hover:shadow-[0_0_25px_var(--color-accent),0_0_50px_var(--color-accent),0_0_100px_var(--color-accent)] transition-shadow duration-500"
					/>
				</div>
			</div>
		{/if}

		<!-- Content -->
		<div class="flex-1 text-center lg:text-left">
			{#if visible}
				<h2
					class="text-4xl md:text-5xl lg:text-6xl font-bold mb-6"
					in:fly={{ y: 40, duration: 600, easing: cubicOut }}
				>
					About <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Me</span>
				</h2>
				<p
					class="text-base md:text-lg leading-relaxed opacity-90"
					in:fly={{ y: 40, duration: 600, delay: 150, easing: cubicOut }}
				>
					I first got into programming at a very young age where I was a Lore team member on a RPG Minecraft server, using JSON to make quests for the RPG content.
					Then in high school, I took a class which covered the basics of HTML and CSS and I absolutely fell in love. After high school I enlisted in the US Army as a 35T (essentially the network guy for the intelligence community).
					After the army I worked in various fields including finish construction, and a Pool Technician job. In both of these fields I refined my attention to detail that I obtained in the military, and learned how to problem solve unusual issues that I come across.
				</p>
				<p
					class="text-base md:text-lg leading-relaxed opacity-90 mt-4"
					in:fly={{ y: 40, duration: 600, delay: 300, easing: cubicOut }}
				>
					Below this about section, you will find two sections: one for the skills I feel solid in and/or have certifications in, and one for the skills I am still learning / obtaining certifications in.
				</p>
			{/if}
		</div>
	</div>
</section>
