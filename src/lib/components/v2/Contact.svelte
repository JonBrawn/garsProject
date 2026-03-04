<script lang="ts">
	import { fly, fade } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	let sectionEl: HTMLElement | undefined = $state();
	let visible = $state(false);

	$effect(() => {
		if (!sectionEl) return;
		const observer = new IntersectionObserver(([entry]) => {
			if (entry.isIntersecting) { visible = true; observer.disconnect(); }
		}, { threshold: 0.1 });
		observer.observe(sectionEl);
		return () => observer.disconnect();
	});
</script>

<section id="contact" class="relative min-h-[80vh] px-6 lg:px-10 py-24 bg-[var(--color-bg)] overflow-hidden" bind:this={sectionEl}>
	<div class="absolute top-0 left-0 w-full h-px bg-gradient-to-r from-transparent via-[var(--color-gradient-two)]/20 to-transparent"></div>

	<!-- Massive glow -->
	<div class="absolute bottom-0 left-1/2 -translate-x-1/2 w-[800px] h-[400px] bg-[var(--color-gradient-one)]/10 rounded-full blur-[150px] pointer-events-none"></div>

	<div class="max-w-5xl mx-auto relative z-10">
		{#if visible}
			<!-- Header -->
			<div class="flex items-end gap-6 mb-12" in:fly={{ y: 50, duration: 700, easing: cubicOut }}>
				<span class="text-[120px] md:text-[180px] font-black leading-none text-[var(--color-text)]/[0.03] select-none">05</span>
				<div class="mb-4">
					<span class="text-xs font-bold tracking-[0.3em] uppercase text-[var(--color-gradient-one)]">Get In Touch</span>
					<h2 class="text-4xl md:text-5xl font-black mt-1">Let's <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Talk</span></h2>
				</div>
			</div>

			<div class="grid lg:grid-cols-[1fr_1.5fr] gap-12" in:fly={{ y: 40, duration: 600, delay: 200, easing: cubicOut }}>
				<!-- Left: Info -->
				<div class="space-y-8">
					<p class="text-base text-[var(--color-text)]/50 leading-relaxed">
						Have an idea, a question, or just want to connect? Drop me a message and I'll get back to you as soon as possible.
					</p>

					<div class="space-y-4">
						<div class="group flex items-center gap-4 p-4 rounded-2xl hover:bg-white/[0.03] transition-colors duration-300">
							<div class="w-12 h-12 rounded-xl bg-[var(--color-gradient-one)]/10 flex items-center justify-center group-hover:shadow-[0_0_20px_var(--color-gradient-one)]/20 transition-all duration-300">
								<i class="bx bx-envelope text-xl text-[var(--color-gradient-one)]"></i>
							</div>
							<div>
								<div class="text-xs text-[var(--color-text)]/30 uppercase tracking-wider font-semibold">Email</div>
								<div class="text-sm font-medium">hello@garrett.dev</div>
							</div>
						</div>
						<div class="group flex items-center gap-4 p-4 rounded-2xl hover:bg-white/[0.03] transition-colors duration-300">
							<div class="w-12 h-12 rounded-xl bg-[var(--color-gradient-one)]/10 flex items-center justify-center group-hover:shadow-[0_0_20px_var(--color-gradient-one)]/20 transition-all duration-300">
								<i class="bx bx-map text-xl text-[var(--color-gradient-one)]"></i>
							</div>
							<div>
								<div class="text-xs text-[var(--color-text)]/30 uppercase tracking-wider font-semibold">Location</div>
								<div class="text-sm font-medium">United States</div>
							</div>
						</div>
					</div>
				</div>

				<!-- Right: Form -->
				<form action="#" class="space-y-4">
					<div class="grid grid-cols-1 md:grid-cols-2 gap-4">
						<div class="group relative">
							<input
								type="text"
								placeholder="Name"
								class="w-full px-5 py-4 text-sm bg-white/[0.03] rounded-2xl border border-white/5 outline-none text-[var(--color-text)] placeholder:text-[var(--color-text)]/20 focus:border-[var(--color-gradient-one)]/50 focus:shadow-[0_0_30px_var(--color-gradient-one)]/10,inset_0_0_30px_var(--color-gradient-one)]/5 transition-all duration-300"
							/>
						</div>
						<div class="group relative">
							<input
								type="email"
								placeholder="Email"
								class="w-full px-5 py-4 text-sm bg-white/[0.03] rounded-2xl border border-white/5 outline-none text-[var(--color-text)] placeholder:text-[var(--color-text)]/20 focus:border-[var(--color-gradient-one)]/50 focus:shadow-[0_0_30px_var(--color-gradient-one)]/10 transition-all duration-300"
							/>
						</div>
					</div>
					<input
						type="text"
						placeholder="Subject"
						class="w-full px-5 py-4 text-sm bg-white/[0.03] rounded-2xl border border-white/5 outline-none text-[var(--color-text)] placeholder:text-[var(--color-text)]/20 focus:border-[var(--color-gradient-one)]/50 focus:shadow-[0_0_30px_var(--color-gradient-one)]/10 transition-all duration-300"
					/>
					<textarea
						placeholder="Your message..."
						rows={5}
						class="w-full px-5 py-4 text-sm bg-white/[0.03] rounded-2xl border border-white/5 outline-none resize-none text-[var(--color-text)] placeholder:text-[var(--color-text)]/20 focus:border-[var(--color-gradient-one)]/50 focus:shadow-[0_0_30px_var(--color-gradient-one)]/10 transition-all duration-300"
					></textarea>

					<button
						type="submit"
						class="group relative inline-flex items-center gap-3 px-8 py-4 rounded-2xl text-sm font-bold uppercase tracking-[0.15em] cursor-pointer overflow-hidden border-none"
					>
						<!-- Button glow bg -->
						<div class="absolute inset-0 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] transition-all duration-300"></div>
						<div class="absolute inset-0 bg-gradient-to-r from-[var(--color-gradient-one)] to-[var(--color-gradient-two)] opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
						<div class="absolute inset-0 shadow-[0_0_40px_var(--color-gradient-one)]/0 group-hover:shadow-[0_0_40px_var(--color-gradient-one)]/40 transition-all duration-500"></div>

						<span class="relative z-10 text-[var(--color-btn-text)]">Send Message</span>
						<i class="bx bx-send relative z-10 text-lg text-[var(--color-btn-text)] group-hover:translate-x-1 group-hover:-translate-y-1 transition-transform duration-300"></i>
					</button>
				</form>
			</div>
		{/if}
	</div>
</section>
