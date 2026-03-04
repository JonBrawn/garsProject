<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade } from 'svelte/transition';
	import { cubicOut } from 'svelte/easing';

	let scrolled = $state(false);
	let scrollProgress = $state(0);
	let mobileMenuOpen = $state(false);
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
			const docHeight = document.documentElement.scrollHeight - window.innerHeight;
			scrollProgress = docHeight > 0 ? window.scrollY / docHeight : 0;

			const sections = navLinks.map((l) => document.getElementById(l.id)).filter(Boolean) as HTMLElement[];
			for (let i = sections.length - 1; i >= 0; i--) {
				if (sections[i].getBoundingClientRect().top <= 150) {
					activeSection = sections[i].id;
					break;
				}
			}
		};
		window.addEventListener('scroll', handleScroll, { passive: true });
		return () => window.removeEventListener('scroll', handleScroll);
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
	}
</script>

<!-- Scroll progress bar -->
<div
	class="fixed top-0 left-0 h-[3px] z-[60] bg-gradient-to-r from-[var(--color-gradient-two)] via-[var(--color-gradient-one)] to-[var(--color-gradient-two)] shadow-[0_0_10px_var(--color-gradient-one),0_0_20px_var(--color-gradient-one)]"
	style="width: {scrollProgress * 100}%"
></div>

<header
	class="fixed top-0 left-0 w-full z-50 transition-all duration-500
		{scrolled ? 'py-2' : 'py-4'}"
>
	<!-- Glassmorphism bg -->
	<div class="absolute inset-0 bg-[var(--color-bg)]/60 backdrop-blur-2xl border-b border-white/5 {scrolled ? 'opacity-100' : 'opacity-0'} transition-opacity duration-500"></div>

	<div class="relative max-w-7xl mx-auto px-6 lg:px-10 flex items-center justify-between">
		{#if mounted}
			<!-- Glitch logo -->
			<a
				href="#home"
				class="group relative text-2xl font-black tracking-tighter"
				in:fly={{ x: -30, duration: 700, easing: cubicOut }}
			>
				<span class="relative z-10 bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">
					GB
				</span>
				<span class="absolute inset-0 bg-gradient-to-r from-[var(--color-gradient-one)] to-[var(--color-gradient-two)] bg-clip-text text-transparent opacity-0 group-hover:opacity-70 translate-x-[2px] translate-y-[2px] transition-all duration-150 group-hover:animate-[glitch_0.3s_ease_infinite]">
					GB
				</span>
				<span class="absolute inset-0 bg-gradient-to-r from-cyan-400 to-blue-400 bg-clip-text text-transparent opacity-0 group-hover:opacity-50 -translate-x-[2px] -translate-y-[1px] transition-all duration-150 group-hover:animate-[glitch_0.3s_ease_infinite_0.15s]">
					GB
				</span>
			</a>

			<!-- Desktop nav -->
			<nav class="hidden lg:flex items-center">
				{#each navLinks as link, i}
					<a
						href={link.href}
						class="group relative px-4 py-2 text-sm font-medium transition-colors duration-300
							{activeSection === link.id ? 'text-[var(--color-gradient-one)]' : 'text-[var(--color-nav-text)]/50 hover:text-[var(--color-nav-text)]'}"
						in:fly={{ y: -20, duration: 400, delay: i * 60, easing: cubicOut }}
					>
						{link.label}
						<!-- Underline glow -->
						<span class="absolute bottom-0 left-1/2 -translate-x-1/2 h-[2px] bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] rounded-full transition-all duration-300 shadow-[0_0_8px_var(--color-gradient-one)]
							{activeSection === link.id ? 'w-full' : 'w-0 group-hover:w-1/2'}"></span>
					</a>
				{/each}
			</nav>

			<div class="flex items-center gap-3">
				<button
					class="w-9 h-9 rounded-full border border-white/10 flex items-center justify-center text-[var(--color-nav-text)]/60 hover:text-[var(--color-gradient-one)] hover:border-[var(--color-gradient-one)]/50 hover:shadow-[0_0_15px_var(--color-gradient-one)]/20 transition-all duration-300 cursor-pointer bg-transparent"
					onclick={toggleTheme}
					aria-label="Toggle theme"
					in:fly={{ y: -20, duration: 400, delay: 400, easing: cubicOut }}
				>
					<i class="bx {theme === 'dark' ? 'bx-sun' : 'bx-moon'} text-base"></i>
				</button>

				<a
					href="#contact"
					class="hidden lg:inline-flex text-xs px-5 py-2.5 rounded-full border border-[var(--color-gradient-one)]/50 text-[var(--color-gradient-one)] font-bold uppercase tracking-widest hover:bg-[var(--color-gradient-one)] hover:text-[var(--color-btn-text)] hover:shadow-[0_0_30px_var(--color-gradient-one)]/40 transition-all duration-300"
					in:fly={{ y: -20, duration: 400, delay: 500, easing: cubicOut }}
				>
					Hire Me
				</a>

				<button
					class="lg:hidden w-9 h-9 rounded-full border border-white/10 flex items-center justify-center text-[var(--color-nav-text)] cursor-pointer bg-transparent"
					onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
					aria-label="Menu"
				>
					<i class="bx {mobileMenuOpen ? 'bx-x' : 'bx-menu'} text-lg"></i>
				</button>
			</div>
		{/if}
	</div>

	{#if mobileMenuOpen}
		<div class="lg:hidden absolute top-full left-0 w-full bg-[var(--color-bg)]/95 backdrop-blur-2xl border-t border-white/5" transition:fly={{ y: -20, duration: 250 }}>
			<nav class="flex flex-col p-6 gap-1">
				{#each navLinks as link, i}
					<a
						href={link.href}
						class="py-3 px-4 text-base font-medium rounded-lg transition-all duration-200
							{activeSection === link.id ? 'text-[var(--color-gradient-one)] bg-[var(--color-gradient-one)]/10' : 'text-[var(--color-nav-text)]/60 hover:text-[var(--color-nav-text)]'}"
						onclick={() => (mobileMenuOpen = false)}
						in:fly={{ x: -20, duration: 200, delay: i * 40 }}
					>
						{link.label}
					</a>
				{/each}
			</nav>
		</div>
	{/if}
</header>
