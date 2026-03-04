<script lang="ts">
	import { fly, fade } from 'svelte/transition';
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
			{ threshold: 0.15 }
		);
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section
	id="contact"
	class="relative min-h-[80vh] px-6 lg:px-10 py-24 bg-[var(--color-bg)] overflow-hidden"
	bind:this={sectionEl}
>
	<div class="absolute bottom-0 left-1/2 -translate-x-1/2 w-[600px] h-[600px] bg-[var(--color-gradient-two)]/10 rounded-full blur-[180px] pointer-events-none"></div>

	<div class="max-w-4xl mx-auto relative z-10">
		{#if visible}
			<div class="text-center mb-12" in:fly={{ y: 40, duration: 600, easing: cubicOut }}>
				<span class="inline-block text-xs font-semibold tracking-[0.2em] uppercase text-[var(--color-gradient-one)] mb-3">Get in touch</span>
				<h2 class="text-4xl md:text-5xl lg:text-6xl font-bold">
					Let's <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Connect</span>
				</h2>
				<p class="text-[var(--color-text)]/60 mt-4 max-w-md mx-auto">Have a project in mind or just want to say hello? I'd love to hear from you.</p>
			</div>

			<form
				action="#"
				class="p-8 md:p-10 rounded-3xl bg-white/5 border border-white/10 backdrop-blur-sm"
				in:fly={{ y: 40, duration: 600, delay: 150, easing: cubicOut }}
			>
				<div class="grid grid-cols-1 md:grid-cols-2 gap-5 mb-5">
					<div class="group">
						<!-- svelte-ignore a11y_label_has_associated_control -->
					<label class="block text-xs font-semibold tracking-wider uppercase text-[var(--color-text)]/40 mb-2 group-focus-within:text-[var(--color-gradient-one)] transition-colors">Name</label>
						<input
							type="text"
							placeholder="John Doe"
							class="w-full px-5 py-3.5 text-sm text-[var(--color-text)] bg-white/5 rounded-xl border border-white/10 outline-none focus:border-[var(--color-accent)]/50 focus:bg-white/10 focus:shadow-[0_0_20px_var(--color-accent)]/10 transition-all duration-300 placeholder:text-[var(--color-text)]/20"
						/>
					</div>
					<div class="group">
						<!-- svelte-ignore a11y_label_has_associated_control -->
					<label class="block text-xs font-semibold tracking-wider uppercase text-[var(--color-text)]/40 mb-2 group-focus-within:text-[var(--color-gradient-one)] transition-colors">Email</label>
						<input
							type="email"
							placeholder="john@example.com"
							class="w-full px-5 py-3.5 text-sm text-[var(--color-text)] bg-white/5 rounded-xl border border-white/10 outline-none focus:border-[var(--color-accent)]/50 focus:bg-white/10 focus:shadow-[0_0_20px_var(--color-accent)]/10 transition-all duration-300 placeholder:text-[var(--color-text)]/20"
						/>
					</div>
					<div class="group">
						<!-- svelte-ignore a11y_label_has_associated_control -->
					<label class="block text-xs font-semibold tracking-wider uppercase text-[var(--color-text)]/40 mb-2 group-focus-within:text-[var(--color-gradient-one)] transition-colors">Phone</label>
						<input
							type="tel"
							placeholder="+1 (555) 000-0000"
							class="w-full px-5 py-3.5 text-sm text-[var(--color-text)] bg-white/5 rounded-xl border border-white/10 outline-none focus:border-[var(--color-accent)]/50 focus:bg-white/10 focus:shadow-[0_0_20px_var(--color-accent)]/10 transition-all duration-300 placeholder:text-[var(--color-text)]/20"
						/>
					</div>
					<div class="group">
						<!-- svelte-ignore a11y_label_has_associated_control -->
					<label class="block text-xs font-semibold tracking-wider uppercase text-[var(--color-text)]/40 mb-2 group-focus-within:text-[var(--color-gradient-one)] transition-colors">Subject</label>
						<input
							type="text"
							placeholder="Project inquiry"
							class="w-full px-5 py-3.5 text-sm text-[var(--color-text)] bg-white/5 rounded-xl border border-white/10 outline-none focus:border-[var(--color-accent)]/50 focus:bg-white/10 focus:shadow-[0_0_20px_var(--color-accent)]/10 transition-all duration-300 placeholder:text-[var(--color-text)]/20"
						/>
					</div>
				</div>

				<div class="group mb-6">
					<!-- svelte-ignore a11y_label_has_associated_control -->
					<label class="block text-xs font-semibold tracking-wider uppercase text-[var(--color-text)]/40 mb-2 group-focus-within:text-[var(--color-gradient-one)] transition-colors">Message</label>
					<textarea
						placeholder="Tell me about your project..."
						rows={5}
						class="w-full px-5 py-3.5 text-sm text-[var(--color-text)] bg-white/5 rounded-xl border border-white/10 outline-none resize-none focus:border-[var(--color-accent)]/50 focus:bg-white/10 focus:shadow-[0_0_20px_var(--color-accent)]/10 transition-all duration-300 placeholder:text-[var(--color-text)]/20"
					></textarea>
				</div>

				<button
					type="submit"
					class="group w-full md:w-auto inline-flex items-center justify-center gap-2 px-8 py-4 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] text-[var(--color-btn-text)] rounded-xl text-sm font-semibold hover:shadow-[0_0_40px_var(--color-accent)]/30 hover:scale-[1.02] transition-all duration-300 cursor-pointer"
				>
					Send Message
					<i class="bx bx-send text-lg group-hover:translate-x-1 group-hover:-translate-y-0.5 transition-transform"></i>
				</button>
			</form>
		{/if}
	</div>
</section>
