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
		{ href: '#about', label: 'About Me' },
		{ href: '#projects', label: 'Projects' },
		{ href: '#contact', label: 'Contact' }
	];
</script>

<footer class="bg-[var(--color-bg-secondary)] py-12 px-[8%]">
	<div class="flex justify-center gap-4 mb-8">
		{#each socials as social}
			<a
				href={social.href}
				class="inline-flex items-center justify-center w-11 h-11 rounded-full border-2 border-[var(--color-accent)] text-[var(--color-accent)] text-xl hover:bg-[var(--color-accent)] hover:text-[var(--color-text)] hover:scale-110 hover:-translate-y-1 transition-all duration-300 hover:shadow-[0_0_25px_var(--color-accent)]"
				aria-label={social.label}
			>
				<i class="bx {social.icon}"></i>
			</a>
		{/each}
	</div>

	<ul class="flex flex-wrap justify-center gap-x-6 gap-y-2 mb-8">
		{#each links as link}
			<li>
				<a
					href={link.href}
					class="text-base text-[var(--color-text)] border-b-2 border-transparent hover:border-[var(--color-accent)] transition-all duration-300"
				>
					{link.label}
				</a>
			</li>
		{/each}
	</ul>

	<p class="text-center text-sm opacity-70">
		&copy; Garrett Brown | All Rights Reserved
	</p>
</footer>
