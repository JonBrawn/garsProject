<script lang="ts">
	import Header from '$lib/components/v2/Header.svelte';
	import Hero from '$lib/components/v2/Hero.svelte';
	import About from '$lib/components/v2/About.svelte';
	import Skills from '$lib/components/v2/Skills.svelte';
	import Projects from '$lib/components/v2/Projects.svelte';
	import Contact from '$lib/components/v2/Contact.svelte';
	import Footer from '$lib/components/v2/Footer.svelte';

	const establishedSkills = [
		{
			icon: 'bxl-figma',
			title: 'UI / UX Design',
			description: 'Crafting intuitive and visually compelling user interfaces with a focus on user experience, accessibility, and clean design principles.'
		},
		{
			icon: 'bxl-html5',
			title: 'HTML 5',
			description: 'Building semantic, accessible, and well-structured web pages using modern HTML5 standards and best practices.'
		},
		{
			icon: 'bxl-css3',
			title: 'CSS 3',
			description: 'Styling responsive and beautiful layouts with CSS3 features including Flexbox, Grid, animations, and custom properties.'
		}
	];

	const upcomingSkills = [
		{
			icon: 'bxl-javascript',
			title: 'JavaScript',
			description: 'Learning to build interactive and dynamic web experiences with vanilla JavaScript and modern ES6+ features.'
		},
		{
			icon: 'bx-code-curly',
			title: "Bachelor's in CS",
			description: "Pursuing a Bachelor's degree in Computer Science to deepen understanding of algorithms, data structures, and software engineering."
		},
		{
			icon: 'bxl-python',
			title: 'Python',
			description: 'Expanding into Python for backend development, scripting, data analysis, and general-purpose programming.'
		}
	];
</script>

<svelte:head>
	<title>Garrett Brown | Web Developer — v2</title>
	<meta name="description" content="Garrett Brown - Web Developer Portfolio" />
</svelte:head>

<Header />

<main>
	<Hero />
	<About />
	<Skills id="skills" sectionNum="02" label="What I Know" title="Core" titleAccent="Skills" skills={establishedSkills} />
	<Skills id="upcoming-skills" sectionNum="03" label="What I'm Learning" title="Upcoming" titleAccent="Skills" skills={upcomingSkills} />
	<Projects />
	<Contact />
	<Footer />
</main>
