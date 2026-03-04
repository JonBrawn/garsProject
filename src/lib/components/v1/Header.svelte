<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	let scrolled = $state(false);
	let mobileMenuOpen = $state(false);
	let settingsOpen = $state(false);
	let theme = $state<'dark' | 'light'>('dark');
	let activeSection = $state('home');
	let mounted = $state(false);

	const navLinks = [
		{ href: '#home', label: 'Home', id: 'home' },
		{ href: '#about', label: 'About', id: 'about' },
		{ href: '#skills', label: 'Skills', id: 'skills' },
		{ href: '#upcoming-skills', label: 'Upcoming', id: 'upcoming-skills' },
		{ href: '#projects', label: 'Projects', id: 'projects' },
		{ href: '#contact', label: 'Contact', id: 'contact' }
	];

	onMount(() => {
		mounted = true;
		const saved = localStorage.getItem('theme');
		if (saved === 'light') {
			theme = 'light';
			document.documentElement.setAttribute('data-theme', 'light');
		}

		const handleScroll = () => {
			scrolled = window.scrollY > 50;

			const sections = navLinks.map((l) => document.getElementById(l.id)).filter(Boolean) as HTMLElement[];
			for (let i = sections.length - 1; i >= 0; i--) {
				const rect = sections[i].getBoundingClientRect();
				if (rect.top <= 150) {
					activeSection = sections[i].id;
					break;
				}
			}
		};
		window.addEventListener('scroll', handleScroll, { passive: true });

		const handleClick = (e: MouseEvent) => {
			if (!(e.target as HTMLElement).closest('.settings-wrapper')) settingsOpen = false;
		};
		document.addEventListener('click', handleClick);

		return () => {
			window.removeEventListener('scroll', handleScroll);
			document.removeEventListener('click', handleClick);
		};
	});

	function toggleTheme() {
		if (theme === 'dark') {
			theme = 'light';
			document.documentElement.setAttribute('data-theme', 'light');
			localStorage.setItem('theme', 'light');
		} else {
			theme = 'dark';
			document.documentElement.removeAttribute('data-theme');
			localStorage.setItem('theme', 'dark');
		}
		settingsOpen = false;
	}
</script>

<header
	class="fixed top-0 left-0 w-full z-50 transition-all duration-500
		{scrolled ? 'py-3 bg-[var(--color-header-bg)] backdrop-blur-2xl shadow-[0_4px_30px_rgba(0,0,0,0.3)] border-b border-white/5' : 'py-5 bg-transparent'}"
>
	<div class="max-w-7xl mx-auto px-6 lg:px-10 flex items-center justify-between">
		<!-- Logo -->
		{#if mounted}
			<a
				href="#home"
				class="text-xl font-extrabold tracking-tight hover:scale-105 transition-transform duration-300"
				in:fly={{ x: -30, duration: 600, easing: cubicOut }}
			>
				<span class="text-[var(--color-text)]">G</span><span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">.</span><span class="text-[var(--color-text)] text-sm font-medium ml-1 opacity-60">Brown</span>
			</a>
		{/if}

		<!-- Desktop nav -->
		<nav class="hidden lg:flex items-center gap-1 bg-white/5 backdrop-blur-md rounded-full px-2 py-1.5 border border-white/10">
			{#each navLinks as link, i}
				{#if mounted}
					<a
						href={link.href}
						class="relative text-sm font-medium px-4 py-2 rounded-full transition-all duration-300
							{activeSection === link.id
								? 'text-[var(--color-btn-text)] bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] shadow-[0_0_20px_var(--color-accent)]'
								: 'text-[var(--color-nav-text)]/70 hover:text-[var(--color-nav-text)] hover:bg-white/10'}"
						onclick={() => (mobileMenuOpen = false)}
						in:fly={{ y: -20, duration: 400, delay: i * 60, easing: cubicOut }}
					>
						{link.label}
					</a>
				{/if}
			{/each}
		</nav>

		<!-- Right side -->
		<div class="flex items-center gap-3">
			{#if mounted}
				<!-- Theme toggle -->
				<button
					class="settings-wrapper relative w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-[var(--color-nav-text)]/70 hover:text-[var(--color-nav-text)] hover:bg-white/10 transition-all duration-300 cursor-pointer"
					onclick={toggleTheme}
					aria-label="Toggle theme"
					in:fly={{ y: -20, duration: 400, delay: 400, easing: cubicOut }}
				>
					<i class="bx {theme === 'dark' ? 'bx-sun' : 'bx-moon'} text-lg transition-transform duration-300 {theme === 'dark' ? 'rotate-0' : 'rotate-180'}"></i>
				</button>

				<!-- CTA -->
				<a
					href="#contact"
					class="hidden lg:inline-flex text-sm px-5 py-2.5 rounded-full bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] text-[var(--color-btn-text)] font-semibold hover:shadow-[0_0_30px_var(--color-accent)] hover:scale-105 transition-all duration-300"
					in:fly={{ y: -20, duration: 400, delay: 500, easing: cubicOut }}
				>
					Let's Talk
				</a>

				<!-- Mobile hamburger -->
				<button
					class="lg:hidden w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-[var(--color-nav-text)] cursor-pointer"
					onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
					aria-label="Toggle menu"
				>
					<i class="bx {mobileMenuOpen ? 'bx-x' : 'bx-menu'} text-xl"></i>
				</button>
			{/if}
		</div>
	</div>

	<!-- Mobile nav -->
	{#if mobileMenuOpen}
		<div
			class="lg:hidden absolute top-full left-0 w-full bg-[var(--color-bg)]/95 backdrop-blur-2xl border-t border-white/5 p-6"
			transition:fly={{ y: -20, duration: 300 }}
		>
			<nav class="flex flex-col gap-2">
				{#each navLinks as link, i}
					<a
						href={link.href}
						class="text-base font-medium py-3 px-4 rounded-xl transition-all duration-200
							{activeSection === link.id
								? 'bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] text-[var(--color-btn-text)]'
								: 'text-[var(--color-nav-text)]/70 hover:bg-white/5'}"
						onclick={() => (mobileMenuOpen = false)}
						in:fly={{ x: -20, duration: 250, delay: i * 50 }}
					>
						{link.label}
					</a>
				{/each}
			</nav>
		</div>
	{/if}
</header>
