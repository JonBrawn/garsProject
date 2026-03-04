<script lang="ts">
	import { onMount } from 'svelte';
	import { fly, fade, slide } from 'svelte/transition';

	let scrolled = $state(false);
	let mobileMenuOpen = $state(false);
	let settingsOpen = $state(false);
	let theme = $state<'dark' | 'light'>('dark');

	const navLinks = [
		{ href: '#home', label: 'Home' },
		{ href: '#about', label: 'About' },
		{ href: '#skills', label: 'Skills' },
		{ href: '#upcoming-skills', label: 'Upcoming Skills' },
		{ href: '#projects', label: 'Projects' },
		{ href: '#contact', label: 'Contact' }
	];

	onMount(() => {
		const saved = localStorage.getItem('theme');
		if (saved === 'light') {
			theme = 'light';
			document.documentElement.setAttribute('data-theme', 'light');
		}

		const handleScroll = () => {
			scrolled = window.scrollY > 50;
		};
		window.addEventListener('scroll', handleScroll);

		const handleClick = (e: MouseEvent) => {
			const target = e.target as HTMLElement;
			if (!target.closest('.settings-wrapper')) {
				settingsOpen = false;
			}
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

	function handleNavClick() {
		mobileMenuOpen = false;
	}
</script>

<header
	class="fixed top-0 left-0 w-full z-50 flex items-center justify-between px-[8%] lg:px-[15%] py-5 transition-all duration-300 {scrolled
		? 'bg-[var(--color-header-bg)] backdrop-blur-xl shadow-lg'
		: 'bg-transparent'}"
>
	<a
		href="#home"
		class="text-2xl font-extrabold text-[var(--color-text)] hover:scale-105 transition-transform duration-300"
	>
		Garrett <span class="bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] bg-clip-text text-transparent">Brown</span>
	</a>

	<button
		class="lg:hidden text-3xl text-[var(--color-nav-text)] cursor-pointer bg-transparent border-none"
		onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
		aria-label="Toggle menu"
	>
		<i class="bx {mobileMenuOpen ? 'bx-x' : 'bx-menu'}"></i>
	</button>

	<!-- Desktop nav -->
	<nav class="hidden lg:flex items-center gap-8">
		{#each navLinks as link, i}
			<a
				href={link.href}
				class="text-base font-medium text-[var(--color-nav-text)] border-b-2 border-transparent hover:text-[var(--color-hover)] hover:border-[var(--color-hover)] transition-all duration-300 pb-1"
				style="animation-delay: {i * 80}ms"
			>
				{link.label}
			</a>
		{/each}
	</nav>

	<div class="hidden lg:flex items-center gap-4">
		<a
			href="#contact"
			class="text-sm px-5 py-2.5 rounded-full bg-gradient-to-r from-[var(--color-gradient-two)] to-[var(--color-gradient-one)] text-[var(--color-btn-text)] font-semibold hover:scale-105 transition-transform duration-300 whitespace-nowrap"
		>
			Contact Me
		</a>

		<div class="settings-wrapper relative">
			<button
				class="flex items-center gap-2 cursor-pointer text-[var(--color-nav-text)] bg-transparent border-none hover:opacity-70 transition-opacity"
				onclick={(e) => {
					e.stopPropagation();
					settingsOpen = !settingsOpen;
				}}
				aria-label="Settings"
			>
				<i class="bx bx-cog text-2xl"></i>
			</button>

			{#if settingsOpen}
				<div
					class="absolute right-0 top-[calc(100%+10px)] min-w-[180px] p-2 rounded-xl bg-[var(--color-menu-bg)] backdrop-blur-md border border-[var(--color-accent)] z-50"
					transition:fly={{ y: -10, duration: 200 }}
				>
					<button
						class="w-full flex items-center gap-3 px-3 py-2.5 rounded-lg bg-transparent border-none text-[var(--color-text)] cursor-pointer hover:bg-[var(--color-bg-secondary)] transition-colors duration-200"
						onclick={toggleTheme}
					>
						<i class="bx {theme === 'dark' ? 'bx-sun' : 'bx-moon'} text-xl text-[var(--color-nav-text)]"></i>
						<span class="text-sm text-[var(--color-nav-text)]">
							{theme === 'dark' ? 'Light Mode' : 'Dark Mode'}
						</span>
					</button>
				</div>
			{/if}
		</div>
	</div>

	<!-- Mobile nav -->
	{#if mobileMenuOpen}
		<nav
			class="lg:hidden absolute top-full right-0 w-[70%] max-w-[300px] bg-[var(--color-menu-bg)] backdrop-blur-xl rounded-bl-2xl border-l-2 border-b-2 border-[var(--color-accent)] p-6 flex flex-col gap-1"
			transition:fly={{ x: 100, duration: 300 }}
		>
			{#each navLinks as link, i}
				<a
					href={link.href}
					class="block text-lg text-[var(--color-nav-text)] py-3 border-b border-white/10 hover:text-[var(--color-hover)] transition-colors duration-200"
					onclick={handleNavClick}
					in:fly={{ x: 30, duration: 200, delay: i * 50 }}
				>
					{link.label}
				</a>
			{/each}
			<button
				class="mt-4 flex items-center gap-2 text-[var(--color-nav-text)] bg-transparent border-none cursor-pointer text-base hover:text-[var(--color-hover)] transition-colors"
				onclick={toggleTheme}
			>
				<i class="bx {theme === 'dark' ? 'bx-sun' : 'bx-moon'} text-xl"></i>
				{theme === 'dark' ? 'Light Mode' : 'Dark Mode'}
			</button>
		</nav>
	{/if}
</header>
