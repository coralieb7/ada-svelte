<script>
	import Chart from '../lib/Chart.svelte';
  import Plot from "../lib/Plot.svelte";
  import Ages from "../lib/Ages.svelte";
	import { onMount } from 'svelte';
	let isScrolled = false;
	// Detect scroll event
	onMount(() => {
		const handleScroll = () => {
			isScrolled = window.scrollY > 750;
		};
		window.addEventListener('scroll', handleScroll);
		return () => window.removeEventListener('scroll', handleScroll);
	});

	// Typewriter logic
	let currentTextIndex = 0;
	let displayedText = ' ';
	const texts = [
		'Do you love movies?',
		'What proportion of female characters is portrayed as smart in movies?',
		'What is the impact of the #MeToo movement on the film industry?',
		'How do you think the film industry can be more inclusive?',
		'In your opinion, how are women portrayed in movies?',
		'What are the prime years for an actress?',
		'How many female directors do you know?',
		'Don’t know half of the answers? You are in the right place.'
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

	// Start typing effect on mount
	onMount(() => {
		typeWriter();
	});
  const data = [
    {
      x: [1, 2, 3, 4, 5],
      y: [10, 15, 13, 17, 22],
      type: "hist",
      mode: "markers",
      marker: { color: "blue" },
    },
  ];

  const layout = {
    title: "Example Plot",
    xaxis: { title: "X Axis" },
    yaxis: { title: "Y Axis" },
    responsive: true,
  };

  const config = {
    displayModeBar: true,
    responsive: true,
  };
</script>

<!-- Large Title Section with Image Background -->
<section
	class="relative h-screen bg-cover bg-center"
	style="background-image: url('/img/home.jpg');"
	id="home"
>
	<div class="absolute inset-0 bg-black opacity-40"></div>
	<!-- Dark overlay for readability -->

	<div class="relative z-10 flex h-full flex-col items-center justify-center gap-4">
		<h1 class="text-10xl sm:text-10xl text-center font-extrabold text-white lg:text-8xl">MADAME</h1>
		<p class="mt-4 text-xl text-white" id="anim">{displayedText}</p>
	</div>
</section>

<!-- Navigation Bar -->
<div
	class={`fixed left-0 right-0 top-0 z-20 transition-all duration-300 ${isScrolled ? 'bg-white bg-opacity-80' : 'bg-transparent'}`}
>
	<nav class="flex items-center justify-between px-6 py-4">
		<!-- Left: Project Title -->
		<div class={`text-2xl font-semibold transition ${isScrolled ? 'text-pink-500' : 'text-white'}`}>
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
			<div class="relative group">
				<!-- Main Link -->
				<a
					href="#datastory"
					class={`font-semibold transition hover:text-pink-500 ${isScrolled ? 'text-pink-300' : 'text-white'}`}
					>Datastory</a
				>
				<!-- Dropdown Menu -->
				<div
					class="absolute left-5 mt-2 hidden w-30 rounded-md bg-white shadow-lg group-hover:flex group-hover:flex-col"
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

	<section id="datastory" class="min-h-screen">
		<h2 class="mb-4 text-center text-3xl font-bold">Datastory</h2>
		<div>
			<h3 class="font-custom mb-4 text-xl" style="font-family: 'Roboto', sans-serif;" id="genres">
				Genres
			</h3>
			<!-- Flex container to split the screen into two columns -->
			<div class="flex min-h-screen">
				<!-- Left side: Chart -->
				<div class="w-1/2 pr-4">
					<!-- Adjust width as needed -->
					<Chart />
				</div>

				<!-- Right side: Additional content -->
				<div class="w-1/2 pr-4">
					<!-- Adjust width as needed -->
					<Chart />
				</div>
			</div>
		</div>
    <div>
      <h3 class="font-custom mb-4 text-xl" style="font-family: 'Roboto', sans-serif;" id="world">World</h3>
      <div class="flex min-h-screen">
        <div class="w-1/2 bg-white shadow-md rounded">
          <Plot {data} {layout} {config} />
        </div>
        <div class="w-1/2 bg-white shadow-md rounded">
          <Ages/>
        </div>
        
      </div>
    </div>
    <div>
      <h3 class="font-custom mb-4 text-xl" style="font-family: 'Roboto', sans-serif;" id="characters">Characters</h3>
    </div>
		<p>Your characters content goes here...</p>
		<p></p>
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
