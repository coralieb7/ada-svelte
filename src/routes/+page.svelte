<script>
	import Axis from '../lib/components/race/Chart.svelte';
	import Ages from '../lib/components/Ages.svelte';
	import DirectorsTime from '../lib/components/DirectorsTime.svelte';
	import BechdelRatings from '../lib/components/BechdelRatings.svelte';
	import { onMount } from 'svelte';
	import ChartF from '../lib/components/race/Chart_F.svelte';
	import Boxes from '../lib/components/Boxes.svelte';
	let isScrolled = false;
	// Detect scroll event
	onMount(() => {
		const handleScroll = () => {
			isScrolled = window.scrollY > 750;
		};
		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});

	let displayedText1 = ' ';
	function typeWriter1() {
		const text1 =
			'Imagine this: an actress sits at a table, flipping through a script. She’s been offered a role in a major film, but there’s a catch. Her character has just a few lines—and the most memorable one is: “What do we do now?”. She delivers it to a man in a moment of high tension, waiting for him to decide the next move.';

		let i1 = 1;
		displayedText1 = text1.charAt(0);

		// Typing effect
		function typeNextChar1() {
			displayedText1 += text1.charAt(i1);

			// Check for a period and pause if necessary
			if (text1.charAt(i1) === '.') {
				i1++; // Increment to the next character
				setTimeout(typeNextChar1, 500); // Pause for 500ms after a period
			} else {
				i1++;
				setTimeout(typeNextChar1, 50); // Normal typing speed
			}
		}

		typeNextChar1(); // Start the typing process
	}

	// Start typing effect on mount
	onMount(() => {
		typeWriter1();
	});
	let displayedText2 = ' ';
	// Function to type the next text
	function typeWriter2() {
		const text2 =
			'This line, so popular in movies, encapsulates a troubling trend: women on screen often lack agency, especially in male-directed films. “What Do We Do Now?” is not just the title of our project, but also a call to action—to explore how directors’ genders influence the roles, agency, and portrayal of women in cinema.';

		displayedText2 = '';
		let i2 = 0;
		// Typing effect
		function typeNextChar2() {
			displayedText2 += text2.charAt(i2);

			// Check for a period and pause if necessary
			if (text2.charAt(i2) === '.') {
				i2++; // Increment to the next character
				setTimeout(typeNextChar2, 500); // Pause for 500ms after a period
			} else {
				i2++;
				setTimeout(typeNextChar2, 50); // Normal typing speed
			}
		}
		setTimeout(() => {
			typeNextChar2(); // Start the typing process
		}, 19000);
	}

	// Start typing effect on mount
	onMount(() => {
		typeWriter2();
	});
	let displayedText3 = ' ';

	// Function to type the next text
	function typeWriter3() {
		const text3 =
			'Through this project, we use data to uncover patterns in representation, challenge stereotypes, and highlight the stories that directors choose to tell about women.';

		let i3 = 0;
		displayedText3 = '';
		// Typing effect
		function typeNextChar3() {
			displayedText3 += text3.charAt(i3);

			// Check for a period and pause if necessary
			if (text3.charAt(i3) === '.') {
				i3++; // Increment to the next character
				setTimeout(typeNextChar3, 500); // Pause for 500ms after a period
			} else {
				i3++;
				setTimeout(typeNextChar3, 50); // Normal typing speed
			}
		}
		setTimeout(() => {
			typeNextChar3(); // Start the typing process
		}, 37000);
	}

	// Start typing effect on mount
	onMount(() => {
		typeWriter3();
	});
</script>

<!-- Large Title Section with Animated Bubbles Background -->
<!-- Large Title Section with Animated Bubbles Background -->
<section class="relative h-screen overflow-hidden bg-black" id="home">
	<!-- Left spotlight -->
	<div class="spotlight-left-container">
		<div class="gradient-line gradient-line-left"></div>
		<div class="spotlight spotlight-left"></div>
	  </div>
	
	  <!-- Right spotlight -->
	  <div class="spotlight-right-container">
		<div class="gradient-line gradient-line-right"></div>
		<div class="spotlight spotlight-right"></div>
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
			{displayedText1}
		</p>
		<p
			class="mt-4 max-w-4xl text-justify text-lg leading-relaxed text-white sm:text-xl lg:text-2xl"
		>
			{displayedText2}
		</p>
		<p
			class="mt-4 max-w-4xl text-justify text-lg leading-relaxed text-white sm:text-xl lg:text-2xl"
		>
			{displayedText3}
		</p>
	</div>
</section>

<!-- Navigation Bar -->
<div
	class={`fixed left-0 right-0 top-0 z-20 transition-all duration-300 ${isScrolled ? 'bg-white bg-opacity-100' : 'bg-transparent'}`}
>
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
<div class="space-y-20 p-6">
	<section id="intro" class="min-h-screen">
		<h2 class="mb-4 text-center text-3xl font-bold">Intro</h2>
		<p>Your introduction content goes here...</p>
	</section>

	<section id="research-questions" class="min-h-screen">
		<h2 class="mb-4 text-center text-3xl font-bold">Research Questions</h2>
		<p>Your research questions content goes here...</p>
	</section>

	<section id="datastory" class="flex min-h-screen flex-col">
		<h2 class="mb-4 text-center font-serif text-3xl" style="font-family: 'Limelight'">MADAME</h2>
		<div>
			<h3 class="font-custom mb-4 text-xl" style="font-family: 'Roboto', sans-serif;" id="genres">
				Genres
			</h3>
			<div class="flex items-center justify-center">
				<!-- <ChartF /> -->
			</div>
			<div class="flex items-center justify-center">
				<BechdelRatings />
			</div>
			<div class="flex items-center justify-center">
				<DirectorsTime />
			</div>
			<div>
				<h3 class="font-custom mb-4 text-xl" style="font-family: 'Roboto', sans-serif;" id="world">
					World
				</h3>
				<div class="flex items-center justify-center">
					<div class="rounded bg-white p-4 shadow-md">
						<Ages />
					</div>
				</div>
			</div>
			<div>
				<h3
					class="font-custom mb-4 text-xl"
					style="font-family: 'Roboto', sans-serif;"
					id="characters"
				>
					Characters
				</h3>
				<div class="flex items-center justify-center">
					<div class="rounded bg-white p-4 shadow-md">
						<Boxes />
					</div>
				</div>
			</div>
			<p>Your characters content goes here...</p>
			<p></p>
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
