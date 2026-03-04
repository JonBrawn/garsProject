<script lang="ts">
	import Header from '$lib/components/v1/Header.svelte';
	import Hero from '$lib/components/v1/Hero.svelte';
	import About from '$lib/components/v1/About.svelte';
	import Skills from '$lib/components/v1/Skills.svelte';
	import Projects from '$lib/components/v1/Projects.svelte';
	import Contact from '$lib/components/v1/Contact.svelte';
	import Footer from '$lib/components/v1/Footer.svelte';

	const establishedSkills = [
		{
			icon: 'bxl-figma',
			title: 'UI / UX Design',
			description: 'Crafting intuitive and visually compelling user interfaces with a focus on user experience, accessibility, and clean design principles.',
			color: 'pink'
		},
		{
			icon: 'bxl-html5',
			title: 'HTML 5',
			description: 'Building semantic, accessible, and well-structured web pages using modern HTML5 standards and best practices.',
			color: 'orange'
		},
		{
			icon: 'bxl-css3',
			title: 'CSS 3',
			description: 'Styling responsive and beautiful layouts with CSS3 features including Flexbox, Grid, animations, and custom properties.',
			color: 'blue'
		}
	];

	const upcomingSkills = [
		{
			icon: 'bxl-javascript',
			title: 'JavaScript',
			description: 'Learning to build interactive and dynamic web experiences with vanilla JavaScript and modern ES6+ features.',
			color: 'yellow'
		},
		{
			icon: 'bx-code-curly',
			title: "Bachelor's in CS",
			description: "Pursuing a Bachelor's degree in Computer Science to deepen understanding of algorithms, data structures, and software engineering.",
			color: 'purple'
		},
		{
			icon: 'bxl-python',
			title: 'Python',
			description: 'Expanding into Python for backend development, scripting, data analysis, and general-purpose programming.',
			color: 'green'
		}
	];
</script>

<svelte:head>
	<title>Garrett Brown | Web Developer — v1</title>
	<meta name="description" content="Garrett Brown - Web Developer Portfolio" />
</svelte:head>

<Header />

<main>
	<Hero />
	<About />
	<Skills id="skills" label="What I know" title="My" titleAccent="Skills" skills={establishedSkills} />
	<Skills id="upcoming-skills" label="What I'm learning" title="Upcoming" titleAccent="Skills" skills={upcomingSkills} alternate />
	<Projects />
	<Contact />
	<Footer />
</main>
