<script lang="ts">
	const socials = [
		{ icon: 'bxl-github', href: '#', label: 'GitHub' },
		{ icon: 'bxl-linkedin-square', href: '#', label: 'LinkedIn' },
		{ icon: 'bxl-instagram-alt', href: '#', label: 'Instagram' },
		{ icon: 'bxl-twitter', href: '#', label: 'Twitter' }
	];
</script>

<footer class="relative bg-[var(--color-bg-secondary)] overflow-hidden">
	<div class="absolute top-0 left-0 w-full h-px bg-gradient-to-r from-transparent via-[var(--color-gradient-one)]/20 to-transparent"></div>

	<div class="max-w-6xl mx-auto px-6 lg:px-10 py-16">
		<div class="flex flex-col md:flex-row items-center justify-between gap-8">
			<!-- Logo -->
			<a href="#home" class="group text-3xl font-black tracking-tighter">
				<span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">GB</span>
				<span class="text-[var(--color-text)]/20 text-sm font-light ml-1">/ 2024</span>
			</a>

			<!-- Socials -->
			<div class="flex items-center gap-1">
				{#each socials as social}
					<a
						href={social.href}
						class="group relative w-10 h-10 flex items-center justify-center text-[var(--color-text)]/30 hover:text-[var(--color-gradient-one)] transition-colors duration-300"
						aria-label={social.label}
					>
						<i class="bx {social.icon} text-lg relative z-10"></i>
						<span class="absolute inset-0 rounded-full border border-transparent group-hover:border-[var(--color-gradient-one)]/20 group-hover:shadow-[0_0_15px_var(--color-gradient-one)]/10 scale-0 group-hover:scale-100 transition-all duration-300"></span>
					</a>
				{/each}
			</div>
		</div>

		<div class="mt-10 pt-6 border-t border-white/5 flex flex-col md:flex-row items-center justify-between gap-4">
			<p class="text-xs text-[var(--color-text)]/20 tracking-wider">
				&copy; {new Date().getFullYear()} GARRETT BROWN. ALL RIGHTS RESERVED.
			</p>
			<p class="text-xs text-[var(--color-text)]/10">
				Built with obsessive attention to detail.
			</p>
		</div>
	</div>
</footer>
