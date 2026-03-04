<script lang="ts">
	import { fly } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

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
	id="contact"
	class="min-h-[80vh] px-[8%] lg:px-[15%] py-20 bg-[var(--color-bg)]"
	bind:this={sectionEl}
>
	{#if visible}
		<h2
			class="text-center text-4xl md:text-5xl lg:text-6xl font-bold mb-10"
			in:fly={{ y: 40, duration: 600, easing: cubicOut }}
		>
			Contact <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Me</span>
		</h2>

		<form
			action="#"
			class="flex flex-col lg:flex-row items-stretch justify-center gap-6 max-w-4xl mx-auto mt-10"
			in:fly={{ y: 40, duration: 600, delay: 150, easing: cubicOut }}
		>
			<div class="flex flex-col gap-4 flex-1">
				<input
					type="text"
					placeholder="Full Name"
					class="w-full px-6 py-4 text-base text-[var(--color-text)] bg-[var(--color-box)] rounded-2xl border-2 border-[var(--color-accent)] outline-none focus:shadow-[0_0_15px_var(--color-accent)] transition-shadow duration-300 placeholder:text-[var(--color-text)]/50"
				/>
				<input
					type="email"
					placeholder="Email"
					class="w-full px-6 py-4 text-base text-[var(--color-text)] bg-[var(--color-box)] rounded-2xl border-2 border-[var(--color-accent)] outline-none focus:shadow-[0_0_15px_var(--color-accent)] transition-shadow duration-300 placeholder:text-[var(--color-text)]/50"
				/>
				<input
					type="tel"
					placeholder="Phone Number"
					class="w-full px-6 py-4 text-base text-[var(--color-text)] bg-[var(--color-box)] rounded-2xl border-2 border-[var(--color-accent)] outline-none focus:shadow-[0_0_15px_var(--color-accent)] transition-shadow duration-300 placeholder:text-[var(--color-text)]/50"
				/>
				<input
					type="text"
					placeholder="Subject"
					class="w-full px-6 py-4 text-base text-[var(--color-text)] bg-[var(--color-box)] rounded-2xl border-2 border-[var(--color-accent)] outline-none focus:shadow-[0_0_15px_var(--color-accent)] transition-shadow duration-300 placeholder:text-[var(--color-text)]/50"
				/>
			</div>
			<div class="flex flex-col gap-4 flex-1">
				<textarea
					placeholder="Your Message"
					rows={8}
					class="w-full px-6 py-4 text-base text-[var(--color-text)] bg-[var(--color-box)] rounded-2xl border-2 border-[var(--color-accent)] outline-none resize-none flex-1 focus:shadow-[0_0_15px_var(--color-accent)] transition-shadow duration-300 placeholder:text-[var(--color-text)]/50"
				></textarea>
				<button
					type="submit"
					class="px-8 py-4 bg-[var(--color-accent)] text-[var(--color-btn-text)] rounded-full text-base font-semibold shadow-[0_0_20px_var(--color-accent)] hover:scale-105 hover:shadow-[0_0_25px_var(--color-accent),0_0_50px_var(--color-accent)] transition-all duration-300 cursor-pointer"
				>
					Send Message
				</button>
			</div>
		</form>
	{/if}
</section>
