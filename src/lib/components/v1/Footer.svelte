<script lang="ts">
	const socials = [
		{ icon: 'bxl-github', href: '#', label: 'GitHub' },
		{ icon: 'bxl-linkedin-square', href: '#', label: 'LinkedIn' },
		{ icon: 'bxl-instagram-alt', href: '#', label: 'Instagram' },
		{ icon: 'bxl-twitter', href: '#', label: 'Twitter' }
	];

	const links = [
		{ href: '#', label: 'FAQ' },
		{ href: '#skills', label: 'Skills' },
		{ href: '#upcoming-skills', label: 'Upcoming Skills' },
		{ href: '#about', label: 'About' },
		{ href: '#projects', label: 'Projects' },
		{ href: '#contact', label: 'Contact' }
	];
</script>

<footer class="relative bg-[var(--color-bg-secondary)] border-t border-white/5 overflow-hidden">
	<div class="absolute bottom-0 left-1/2 -translate-x-1/2 w-96 h-32 bg-[var(--color-gradient-two)]/10 rounded-full blur-[100px] pointer-events-none"></div>

	<div class="max-w-6xl mx-auto px-6 lg:px-10 py-16 relative z-10">
		<div class="flex flex-col md:flex-row items-center md:items-start justify-between gap-10">
			<!-- Brand -->
			<div class="text-center md:text-left">
				<a href="#home" class="text-2xl font-extrabold">
					<span class="text-[var(--color-text)]">G</span><span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">.</span><span class="text-[var(--color-text)] text-sm font-medium ml-1 opacity-60">Brown</span>
				</a>
				<p class="text-sm text-[var(--color-text)]/40 mt-2 max-w-xs">Building the web, one project at a time.</p>
			</div>

			<!-- Links -->
			<div class="flex flex-wrap justify-center gap-x-8 gap-y-3">
				{#each links as link}
					<a
						href={link.href}
						class="text-sm text-[var(--color-text)]/50 hover:text-[var(--color-text)] transition-colors duration-300"
					>
						{link.label}
					</a>
				{/each}
			</div>

			<!-- Socials -->
			<div class="flex gap-3">
				{#each socials as social}
					<a
						href={social.href}
						class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-[var(--color-text)]/50 hover:bg-[var(--color-accent)] hover:text-[var(--color-btn-text)] hover:border-[var(--color-accent)] hover:scale-110 hover:-translate-y-1 hover:shadow-[0_0_20px_var(--color-accent)]/50 transition-all duration-300"
						aria-label={social.label}
					>
						<i class="bx {social.icon} text-lg"></i>
					</a>
				{/each}
			</div>
		</div>

		<!-- Divider -->
		<div class="mt-12 pt-6 border-t border-white/5 text-center">
			<p class="text-xs text-[var(--color-text)]/30">
				&copy; {new Date().getFullYear()} Garrett Brown. All Rights Reserved.
			</p>
		</div>
	</div>
</footer>
