<script>
	import Ages from '../lib/components/Ages.svelte';
	import DirectorsTime from '../lib/components/DirectorsTime.svelte';
	import BechdelRatings from '../lib/components/BechdelRatings.svelte';
	import { onMount } from 'svelte';
	import Chart from '$lib/components/race/Chart.svelte';
	import Boxes from '../lib/components/Boxes.svelte';
	import RendementsOpti from '$lib/components/Rendements_opti.svelte';
	import RendementsWorst from '$lib/components/Rendements_worst.svelte';
	import AverageRatingsOpti from '$lib/components/AverageRatingsOpti.svelte';
	import AverageRatingsWorst from '$lib/components/AverageRatingsWorst.svelte';

	
	// for the scroll
	let isScrolled = false;
	let firstBubbleVisible = false;
	let secondBubbleVisible = false;
	let thirdBubbleVisible = false;
	onMount(() => {
		const handleScroll = () => {
			isScrolled = window.scrollY > 750;
			firstBubbleVisible = window.scrollY > 800;
			secondBubbleVisible = window.scrollY > 820;
			thirdBubbleVisible = window.scrollY > 840;
		};
		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});

	let currentTextIndex = 0;
	let displayedText = ' ';
	const texts = [
		'How do directors frame women?',
		'Do female directors rewrite stereotypes?',
		'Are female characters more than tropes?',
		'Why do women in films so often ask, "What do we do now?" instead of deciding?'
	];

	// Function to type the next text
	function typeWriter() {
		const text = texts[currentTextIndex];
		let i = 1;
		displayedText = text.charAt(0);

		// Typing effect
		const interval = setInterval(() => {
			if (i < text.length) {
				displayedText += text.charAt(i);
				i++;
			} else {
				clearInterval(interval); // Stop the typing when the text is fully typed
				setTimeout(() => {
					currentTextIndex = (currentTextIndex + 1) % texts.length;
					typeWriter(); // Call it again for the next text
				}, 2000); // Wait for 1 second before typing the next text
			}
		}, 50); // Speed of typing (adjust if needed)
	}
	onMount(() => {
		typeWriter();
	});
</script>

<section class="relative h-screen overflow-hidden bg-black" id="home">
	<!-- Left spotlight -->
	<div class="spotlight-left-container">
		<div class="gradient-line-left"></div>
		<div class="spotlight-left"></div>
	</div>

	<!-- Right spotlight -->
	<div class="spotlight-right-container">
		<div class="gradient-line-right"></div>
		<div class="spotlight-right"></div>
	</div>

	<!-- Content -->
	<div class="relative z-10 flex h-full flex-col items-center justify-center gap-4">
		<h1
			class="text-center text-6xl font-extrabold text-white sm:text-6xl lg:text-6xl"
			style="font-family: 'Limelight'"
		>
			"WHAT DO WE DO NOW?"
		</h1>
		<p
			class="mt-4 max-w-4xl text-justify text-lg leading-relaxed text-white sm:text-xl lg:text-2xl"
		>
			{displayedText}
		</p>
	</div>
</section>

<!-- Navigation Bar -->
<div class={`fixed left-0 right-0 top-0 z-20 bg-transparent transition-all duration-300`}>
	<nav class="flex items-center justify-between px-6 py-4">
		<!-- Left: Project Title -->
		<div
			class={`text-2xl font-semibold transition ${isScrolled ? 'text-pink-500' : 'text-white'}`}
			style="font-family: 'Limelight'"
		>
			MADAME
		</div>

		<!-- Right: Navigation Links -->
		<div class="flex space-x-4">
			<a
				href="#home"
				class={`font-semibold transition hover:text-pink-500 ${isScrolled ? 'text-pink-300' : 'text-white'}`}
				>Home</a
			>
			<a
				href="#intro"
				class={`font-semibold transition hover:text-pink-500 ${isScrolled ? 'text-pink-300' : 'text-white'}`}
				>Intro</a
			>
			<a
				href="#research-questions"
				class={`font-semibold transition hover:text-pink-500 ${isScrolled ? 'text-pink-300' : 'text-white'}`}
				>Research Questions</a
			>
			<!-- Datastory Item with Dropdown -->
			<div class="group relative">
				<!-- Main Link -->
				<a
					href="#datastory"
					class={`font-semibold transition hover:text-pink-500 ${isScrolled ? 'text-pink-300' : 'text-white'}`}
					>Datastory</a
				>
				<!-- Dropdown Menu -->
				<div
					class="w-30 absolute left-5 mt-2 hidden rounded-md bg-white shadow-lg group-hover:flex group-hover:flex-col"
				>
					<a
						href="#genres"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>Genres</a
					>
					<a
						href="#world"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>World</a
					>
					<a
						href="#characters"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>Characters</a
					>
				</div>
			</div>
			<a
				href="#team"
				class={`font-semibold transition hover:text-pink-500 ${isScrolled ? 'text-pink-300' : 'text-white'}`}
				>Our Team</a
			>
		</div>
	</nav>
</div>

<!-- Content Sections (below the large title) -->
<div class="space-y-20 bg-white p-6">
	<section id="intro" class="relative flex min-h-screen items-center justify-center bg-black">
		<!-- First Bubble -->
		<div
			class="bubble-container-left absolute flex items-center justify-center"
			class:visible={firstBubbleVisible}
		>
			<div class="bubble-content">
				<p class="leading-relaxed text-white">
					Meet Madame. Sitting at her table, she is holding her very first movie script, a huge
					opportunity she’s dreamed about for years. Suddenly, as she flips through the pages, one
					line catches her eye: “WHAT DO WE DO NOW?” …. Why would this easy as pie question disturb
					her so much? Because she delivers it to a man in a moment of high tension, waiting for him
					to decide the next move. Disillusioned, Madame wonders: Is this really how it starts? A
					character with little to say, caught in a moment of indecision, as usual, relying on a man
					to take charge?
				</p>
			</div>
		</div>

		<!-- Second Bubble -->
		<div
			class="bubble-container-right absolute flex items-center justify-center"
			class:visible={secondBubbleVisible}
		>
			<div class="bubble-content">
				<p class="leading-relaxed text-white">
					This iconic line is more than just dialogue. It’s a symbol of a deeper issue: women in
					films are often underrepresented and stereotyped, their roles shaped by limited
					perspectives. “What Do We Do Now?” isn’t just the title of our project—it’s a question
					we’re asking to explore how the gender of a movie director influences how women are
					portrayed on screen.
				</p>
			</div>
		</div>
		<!-- Third Bubble -->
		<div
			class="bubble-container-left2 absolute flex items-center justify-center"
			class:visible={thirdBubbleVisible}
		>
			<div class="bubble-content">
				<p class="leading-relaxed text-white">
					Through our analysis, we’ll explore how the gender of a director influences female
					representation, uncover the stereotypes that still dominate, and track how women’s roles
					have evolved across time and cultures. Because some questions raised in cinema do not
					always stay on screen : they reflect real-world dynamics, mirroring how groups of people
					and behaviors are portrayed in our society.
				</p>
			</div>
		</div>
	</section>

	<section id="research-questions" class="min-h-screen">
		<h2 class="mb-4 text-center text-3xl font-bold text-white">Research Questions</h2>
		<p>Your research questions content goes here...</p>
	</section>

	<section id="datastory" class="flex min-h-screen flex-col">
		<h2 class="mb-4 text-center font-serif text-3xl text-white" style="font-family: 'Limelight'">
			MADAME
		</h2>
		<div>
			<h3 class="font-custom mb-4 text-xl text-black" id="genres">Genres</h3>
			<div class="flex flex-row items-center justify-center">
				<Chart />
			</div>
		</div>
		<div>
			<h3 class="font-custom mb-4 text-xl text-white" id="world">World</h3>
			<div class="flex flex-col items-center justify-center">
				<div class="rounded bg-white p-4 shadow-md">
					<Ages />
				</div>
				<div class="flex items-center justify-center">
					<BechdelRatings />
				</div>
				<div class="flex items-center justify-center">
					<DirectorsTime />
				</div>
				<div class="flex items-center justify-center">
					<RendementsOpti />
				</div>
				<div class="flex items-center justify-center">
					<RendementsWorst />
				</div>
				<div class="flex items-center justify-center">
					<AverageRatingsOpti />
				</div>
				<div class="flex items-center justify-center">
					<AverageRatingsWorst />
				</div>
			</div>
		</div>
		<div>
			<h3 class="font-custom mb-4 text-xl text-white" id="characters">Characters</h3>
			<div class="flex items-center justify-center">
				<div class="rounded bg-white p-4 shadow-md">
					<Boxes />
				</div>
			</div>
		</div>
	</section>

	<section id="team" class="min-h bg-gray-100 py-8">
		<h2 class="mb-4 text-center text-3xl font-bold">Our Team</h2>
		<!-- Team Member Info Here -->
		<!-- Team Members -->
		<div class="grid grid-cols-1 gap-6 text-center md:grid-cols-5">
			<div>
				<h3 class="text-lg font-semibold">Mahlia Merville</h3>
				<p class="text-sm">Role or Title</p>
			</div>
			<div>
				<h3 class="text-lg font-semibold">Pernelle Paget</h3>
				<p class="text-sm">Role or Title</p>
			</div>
			<div>
				<h3 class="text-lg font-semibold">Coralie Banuls</h3>
				<p class="text-sm">Role or Title</p>
			</div>
			<div>
				<h3 class="text-lg font-semibold">Juliette Le Béchec</h3>
				<p class="text-sm">Role or Title</p>
			</div>
			<div>
				<h3 class="text-lg font-semibold">Maximilien Gridel</h3>
				<p class="text-sm">Role or Title</p>
			</div>
		</div>
	</section>
</div>
