<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade, scale } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';
	import { base } from '$app/paths';

	let visible = $state(false);

	const socials = [
		{ icon: 'bxl-github', href: '#', label: 'GitHub' },
		{ icon: 'bxl-linkedin-square', href: '#', label: 'LinkedIn' },
		{ icon: 'bxl-instagram-alt', href: '#', label: 'Instagram' },
		{ icon: 'bxl-twitter', href: '#', label: 'Twitter' }
	];

	onMount(() => {
		visible = true;
	});
</script>

<section id="home" class="min-h-screen flex items-center justify-center px-[8%] lg:px-[15%] pt-28 pb-16">
	<div class="flex flex-col-reverse lg:flex-row items-center justify-center gap-12 lg:gap-24 w-full max-w-6xl">
		<!-- Text -->
		<div class="flex flex-col items-center lg:items-end text-center lg:text-right flex-1">
			{#if visible}
				<h1
					class="text-5xl md:text-6xl lg:text-7xl font-bold leading-tight"
					in:fly={{ y: 40, duration: 700, easing: cubicOut }}
				>
					Hi, It's <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Garrett</span>
				</h1>

				<h3
					class="text-2xl md:text-3xl lg:text-4xl font-semibold mt-3"
					in:fly={{ y: 40, duration: 700, delay: 150, easing: cubicOut }}
				>
					I'm a <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Web Developer</span>
				</h3>

				<p
					class="text-sm md:text-base font-medium leading-relaxed mt-5 max-w-lg opacity-85"
					in:fly={{ y: 40, duration: 700, delay: 300, easing: cubicOut }}
				>
					Welcome to my portfolio website! Everything you see here is evolving with me as my skills grow and I learn new things.
					Currently I am studying through the freeCodeCamp Curriculum, and I have applied to various universities to obtain my Bachelors in Computer Science!
				</p>

				<div
					class="flex gap-3 mt-8"
					in:fly={{ y: 30, duration: 600, delay: 450, easing: cubicOut }}
				>
					{#each socials as social, i}
						<a
							href={social.href}
							class="inline-flex items-center justify-center w-12 h-12 rounded-full border-2 border-[var(--color-accent)] text-[var(--color-accent)] text-xl hover:bg-[var(--color-accent)] hover:text-[var(--color-text)] hover:scale-110 hover:-translate-y-1 transition-all duration-300 hover:shadow-[0_0_25px_var(--color-accent)]"
							aria-label={social.label}
							in:scale={{ start: 0, duration: 400, delay: 550 + i * 80, easing: cubicOut }}
						>
							<i class="bx {social.icon}"></i>
						</a>
					{/each}
				</div>

				<div
					class="mt-6"
					in:fly={{ y: 20, duration: 500, delay: 700, easing: cubicOut }}
				>
					<a
						href="#about"
						class="inline-block px-8 py-3 bg-[var(--color-accent)] text-[var(--color-btn-text)] rounded-full text-base font-semibold shadow-[0_0_20px_var(--color-accent)] hover:scale-105 hover:shadow-[0_0_25px_var(--color-accent),0_0_50px_var(--color-accent)] transition-all duration-300"
					>
						Read More
					</a>
				</div>
			{/if}
		</div>

		<!-- Image -->
		<div class="flex-shrink-0">
			{#if visible}
				<div
					in:scale={{ start: 0.8, duration: 800, delay: 200, easing: cubicOut }}
				>
					<div class="relative group">
						<div class="absolute -inset-1 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] rounded-full blur-md opacity-50 group-hover:opacity-80 transition-opacity duration-500"></div>
						<img
							src="{base}/images/image.jpg"
							alt="Garrett Brown"
							class="relative w-52 h-52 md:w-72 md:h-72 lg:w-80 lg:h-80 rounded-full object-cover shadow-[0_0_25px_var(--color-accent)] group-hover:shadow-[0_0_25px_var(--color-accent),0_0_50px_var(--color-accent),0_0_100px_var(--color-accent)] transition-shadow duration-500"
						/>
					</div>
				</div>
			{/if}
		</div>
	</div>
</section>
