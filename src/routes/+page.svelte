<script>
	import { onMount } from 'svelte';
	import { fly } from 'svelte/transition';
	import { quintOut } from 'svelte/easing';

	import Ages from '../lib/components/Ages.svelte';
	import DirectorsTime from '../lib/components/DirectorsTime.svelte';
	import BechdelRatings from '../lib/components/BechdelRatings.svelte';
	import Chart from '$lib/components/race/Chart.svelte';
	import Boxes from '../lib/components/Boxes.svelte';
	import RendementsOpti from '$lib/components/Rendements_opti.svelte';
	import RendementsWorst from '$lib/components/Rendements_worst.svelte';
	import AverageRatingsOpti from '$lib/components/AverageRatingsOpti.svelte';
	import AverageRatingsWorst from '$lib/components/AverageRatingsWorst.svelte';
	import Emotions from '$lib/components/Emotions.svelte';
	import EmotionsBechdel from '$lib/components/EmotionsBechdel.svelte';
	import GenresM from '$lib/components/genres/GenresMale.svelte';
	import GenresF from '$lib/components/genres/GenresFemale.svelte';

	import Tvtropes from '$lib/components/Tvtropes.svelte';
	import MemoryGame from '$lib/components/MemoryGame.svelte';
	import RatingsBoxOffice from '$lib/components/RatingsBoxOffice.svelte';
	import Revenue from '$lib/components/Revenue.svelte';
	import BechdelCategory from '$lib/components/BechdelCategory.svelte';
	import WordsF from '$lib/components/WordsFemale.svelte';
	import WordsM from '$lib/components/WordsMale.svelte';
	import BechdelCategoryModel from '$lib/components/BechdelCategoryModel.svelte';

	let showBubbles = false;
	let navVisible = true;
	let lastScrollPosition = 0;
	let researchQuestionsVisible = [false, false, false];
	let visibleSections = [false, false, false];
	onMount(() => {
		const handleScroll = () => {
			const homeSection = document.querySelector('#home');
			const conclusionSection = document.querySelector('#conclusion');
			const introSection = document.querySelector('#intro');
			const navBar = document.querySelector('nav');
			const researchQuestionsSection = document.querySelector('#research-questions-datasets');
			if (homeSection) {
				const rect = homeSection.getBoundingClientRect();
				const isVisible =
					rect.top <= window.innerHeight / 2 && rect.bottom >= window.innerHeight / 2;
				if (isVisible) {
					navVisible = true;
				} else {
					navVisible = false;
				}
			}
			if (conclusionSection) {
				const rect = conclusionSection.getBoundingClientRect();
				const isVisible =
					rect.top <= window.innerHeight * 0.7 && rect.bottom >= window.innerHeight * 0.3;

				if (isVisible) {
					// Stagger the appearance of sections
					setTimeout(() => (visibleSections[0] = true), 200);
					setTimeout(() => (visibleSections[1] = true), 600);
					setTimeout(() => (visibleSections[2] = true), 1000);
				}
			}
			if (introSection) {
				const rect = introSection.getBoundingClientRect();

				// Check if intro section is in view
				const isVisible =
					rect.top <= window.innerHeight / 2 && rect.bottom >= window.innerHeight / 2;

				// Show bubbles when intro section is in view
				if (isVisible && !showBubbles) {
					showBubbles = true;
				}

				// Handle navigation bar visibility
				const currentScrollPosition = window.pageYOffset;

				// if (currentScrollPosition > lastScrollPosition) {
				// 	// Scrolling down
				// 	navVisible = currentScrollPosition < 500; // Hide after scrolling down 100px
				// } else {
				// 	// Scrolling up
				// 	navVisible = true;
				// }

				lastScrollPosition = currentScrollPosition;

				// // Apply navigation bar visibility
				// if (navBar) {
				// 	navBar.style.opacity = navVisible ? '1' : '0';
				// 	navBar.style.visibility = navVisible ? 'visible' : 'hidden';
				// }
				// New research questions animation logic
				if (researchQuestionsSection) {
					const questionsRect = researchQuestionsSection.getBoundingClientRect();
					const isQuestionsVisible =
						questionsRect.top <= window.innerHeight * 0.7 &&
						questionsRect.bottom >= window.innerHeight * 0.3;
					if (isQuestionsVisible) {
						// Stagger the appearance of questions
						setTimeout(() => (researchQuestionsVisible[0] = true), 200);
						setTimeout(() => (researchQuestionsVisible[1] = true), 400);
						setTimeout(() => (researchQuestionsVisible[2] = true), 600);
					}
				}
			}
		};

		// Add scroll event listener
		window.addEventListener('scroll', handleScroll);

		// Cleanup event listener on component destruction
		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
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
				}, 3000); // Wait for 1 second before typing the next text
			}
		}, 50); // Speed of typing (adjust if needed)
	}
	onMount(() => {
		typeWriter();
	});
	let hoveredCircle = null;

	const circleData = [
		{ text: 'CMU Movie', link: 'https://www.cs.cmu.edu/~ark/personas/' },
		{ text: 'Bechdel Test', link: 'https://bechdeltest.com/' },
		{ text: 'TV-Tropes', link: 'https://tvtropes.org/' },
		{ text: 'IMDb Ratings', link: 'https://developer.imdb.com/non-commercial-datasets/' },
		{ text: 'TMDB Ratings', link: 'https://ada-svelte.vercel.app' }
	];
	const conclusionParts = [
		"Madame's investigation into the gender dynamics in the film industry has uncovered several key insights: Gender imbalance among directors: Female directors tend to portray more nuanced and diverse female characters compared to their male counterparts. Bechdel Test success: Films that pass the Bechdel Test are more likely to feature strong female representation and emotional depth, especially when directed by women.",
		'Emotional complexity: Stereotypes and societal norms: Common stereotypes in film may be deeply rooted in societal structures, not just industry trends, with certain tropes being more prevalent in films directed by men. Sucess: Movies with strong female representation tend to perform better both critically and at the box office, offering a glimpse of hope for change.',
		"With this newfound knowledge, Madame KNOWS WHAT TO DO NOW. What if she now did not want to play, but actually direct a movie? She now understands the dynamics at play in the industry and, more importantly, how to break free from them. She's determined to step outside the boundaries of Hollywood trends and defy the stereotypes that have long shaped women's roles in cinema."
	];
</script>

<section class="relative h-screen overflow-hidden bg-white" id="home">
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
		<h1 class="text-center text-7xl font-extrabold text-black sm:text-6xl lg:text-6xl">
			"WHAT DO WE DO NOW?"
		</h1>
		<p
			class="mt-4 max-w-4xl text-justify text-lg leading-relaxed text-black sm:text-xl lg:text-2xl"
		>
			{displayedText}
		</p>
	</div>
</section>

<!-- Navigation Bar -->
<div
	class={`fixed left-0 right-0 top-0 z-20 bg-transparent bg-white transition-all duration-300 ${
		navVisible ? 'bg-opacity-10' : 'bg-opacity-100'
	}`}
>
	<nav class="flex items-center justify-between px-6 py-4">
		<!-- Left: Project Title -->
		<a href="#home" class={`text-2xl font-semibold text-black transition`}> MADAME </a>

		<!-- Right: Navigation Links -->
		<div class="flex space-x-4">
			<a href="#intro" class={`font-semibold text-black transition hover:text-emerald-600`}>Intro</a
			>
			<a
				href="#research-questions-datasets"
				class={`font-semibold text-black transition hover:text-violet-500`}
				>Research Questions and Datasets</a
			>

			<!-- Datastory Item with Dropdown -->
			<div class="group relative">
				<!-- Main Link -->
				<a href="#datastory" class={`font-semibold text-black transition hover:text-orange-500`}
					>Datastory</a
				>
				<!-- Dropdown Menu -->
				<div
					class="absolute left-5 mt-2 hidden w-40 rounded-md bg-white shadow-lg group-hover:flex group-hover:flex-col"
				>
					<a
						href="#moviedirectors"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-orange-100 hover:text-orange-500"
						>Gender Distribution</a
					>
					<a
						href="#stereotypes"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-orange-100 hover:text-orange-500"
						>Stereotropes</a
					>
					<a
						href="#bechdeltest"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-orange-100 hover:text-orange-500"
						>Bechdel Test</a
					>
					<a
						href="#success"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-orange-100 hover:text-orange-500"
						>Success</a
					>
				</div>
			</div>
			<a href="#conclusion" class={`font-semibold text-black transition hover:text-yellow-500`}
				>Conclusion</a
			>
			<a href="#team" class={`font-semibold text-black transition hover:text-rose-500`}>Our Team</a>
		</div>
	</nav>
</div>

<!-- Content Sections (below the large title) -->
<div class="space-y-20 bg-white p-6">
	<section class="relative flex min-h-screen justify-center">
		<h2 id="intro" class="mb-4 text-7xl font-bold text-black">INTRODUCTION</h2>
		<!-- First Bubble -->
		<div
			class="bubble-container-left absolute flex items-center justify-center"
			class:visible={showBubbles}
		>
			<div class="bubble-content">
				<p class="leading-relaxed text-black">
					Meet Madame. <br /> Sitting at her table, she is <br />holding her very first movie
					script, a huge<br />
					opportunity she’s dreamed about for years. Suddenly, <br />as she flips through the pages,
					one line catches her eye: <br />“WHAT DO WE DO NOW?” …. Why would this easy as pie
					<br />question disturb her so much? Because she delivers it to a man<br /> in a moment of
					high tension, waiting for him to decide the <br />next move. Madame wonders: Is this
					really how it <br />starts? A character with little to say, caught<br /> in a moment of
					indecision, as usual,<br /> relying on a man to take<br />
					charge?
				</p>
			</div>
		</div>

		<!-- Second Bubble -->
		<div
			class="bubble-container-right absolute flex items-center justify-center"
			class:visible={showBubbles}
		>
			<div class="bubble-content">
				<p class="leading-relaxed text-black">
					This line, so <br />popular in movies, is more than <br />just dialogue. It’s a symbol of
					a deeper issue:<br /> women in films are often underrepresented and <br />stereotyped,
					their roles shaped by limited perspectives.<br /> “What Do We Do Now?”<br /> is not just
					the title of our project: it’s a question we’re <br /> asking to explore how the gender of
					a movie <br />director influences how women are <br />portrayed on screen.
				</p>
			</div>
		</div>
		<!-- Third Bubble -->
		<div
			class="bubble-container-left2 absolute flex items-center justify-center"
			class:visible={showBubbles}
		>
			<div class="bubble-content">
				<p class="leading-relaxed text-black">
					Through this project,<br /> we use data to uncover patterns in <br />representation,
					challenge stereotypes, and<br /> highlight the stories that directors choose to tell about<br
					/>
					women. Because some questions raised in cinema do <br />not always stay on screen : they
					reflect real-world <br />dynamics, mirroring how groups of people <br />and behaviors are
					portrayed<br />
					in our society.
				</p>
			</div>
		</div>
	</section>

	<!-- Research Questions Section-->
	<section
		id="research-questions-datasets"
		class="relative flex flex-col items-center justify-center"
	>
		<div class="flex min-h-screen flex-col items-center justify-center gap-6">
			<div class="flex max-w-5xl flex-col items-center justify-center">
				<h2 class="mb-4 text-7xl font-bold text-black">RESEARCH QUESTIONS</h2>

				<div class="w-full">
					<div class="my-4 h-px bg-violet-700"></div>
					{#each ['How does the gender of a movie director influence the portrayal of women in cinema?', 'What are the key female stereotypes in movies?', 'Are female directors better than men at depicting women in movies?'] as question, index}
						<div
							class="transform transition-all duration-700 ease-out"
							class:opacity-0={!researchQuestionsVisible[index]}
							class:translate-x-[-100%]={!researchQuestionsVisible[index]}
							class:opacity-100={researchQuestionsVisible[index]}
							class:translate-x-0={researchQuestionsVisible[index]}
						>
							{#if index > 0}
								<div class="my-4 h-px bg-violet-700"></div>
							{/if}
							<p class="text-xl text-black">{question}</p>
						</div>
					{/each}
					<div class="my-4 h-px bg-violet-700"></div>
				</div>
			</div>
			<div class="flex flex-col items-center justify-center gap-8 space-x-4">
				<h2 class="relative mb-4 text-7xl font-bold text-black">DATASETS</h2>
				<div class="flex items-center justify-center space-x-4">
					{#each circleData as circle, index}
						<div
							role="button"
							tabindex="0"
							class="relative flex h-48 w-48 items-center justify-center rounded-full border-2 border-emerald-400 transition-all duration-300"
							class:rotate-45={hoveredCircle === index}
							on:mouseenter={() => (hoveredCircle = index)}
							on:mouseleave={() => (hoveredCircle = null)}
						>
							<a
								href={circle.link}
								class="text-center font-semibold text-black"
								target="_blank"
								rel="noopener noreferrer"
							>
								{circle.text}
							</a>
						</div>
					{/each}
				</div>
			</div>
		</div>
	</section>

	<!-- DataStory Section -->
	<section id="datastory" class="flex flex-col items-center justify-center">
		<div class="max-w-5xl">
			<div class="flex flex-col items-center gap-10 py-2">
				<p class=" text-7xl font-bold">DATASTORY</p>
			</div>

			<div
				class="flex flex-col items-center justify-center gap-10 p-8 text-justify"
				id="moviedirectors"
			>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame is speechless, stunned. She never expected that her first major role would be
					reduced to the weak line, "What do we do now?" It feels like a blow to the gut. She can’t
					help but wonder if this cliché is the result of a male director’s influence. If only the
					director had been a woman, maybe her character would have been more complex and
					meaningful. This sparks a realization: are women stereotypes tied to the gender of the
					director?
				</p>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					With these questions in mind, Madame sets off on a quest for answers. Fortunately, the
					Applied Data Analysis (ADA) course she took during her Masters didn't just leave her with
					good memories; it gave her tools. Dusting off her coding skills, She immersed herself in
					the cinema data world.
				</p>
				<h2 class="mb-4 flex justify-start text-5xl font-bold text-black">
					Gender Distribution in Cinema
				</h2>
				<div class="flex flex-row gap-40">
					<div class="flex flex-col items-center">
						<p class="mt-2 text-center text-2xl font-semibold text-yellow-500">Movie Directors</p>
						<div
							class="flex h-80 w-80 bg-cover"
							style="background-image: url('/img/G1.png');"
						></div>
					</div>

					<div class="flex flex-col items-center">
						<p class="mt-2 text-center text-2xl font-semibold text-yellow-500">Characters</p>
						<div
							class="flex h-80 w-80 bg-cover"
							style="background-image: url('/img/G2.png');"
						></div>
					</div>
				</div>
				<p class="bg-yellow-200 p-4 text-xl text-black">
					It doesn't take long for the first revelation to appear, stark and undeniable: the gender
					distribution among film directors is far from balanced. What's more, the gender
					distribution of the movie directors - 90% male, 10% female - is far more contrasted than
					that of the actors: 67% of the actors are male, while the remaining 33% are female.
				</p>
				<div class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					<p>
						Madame suddenly remembers the "Celluloid Ceiling" concept she read about two weeks ago:
						an invisible but powerful barrier that has kept women from reaching key creative roles
						in filmmaking for decades
					</p>
					<a
						href={'https://womenintvfilm.sdsu.edu/wp-content/uploads/2023/01/2022-celluloid-ceiling-report.pdf'}
						class="text-center font-semibold text-black"
						target="_blank"
						>(Lauzen, M. 2022)
					</a>
				</div>

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame’s curiosity grows as she wonders if the gender imbalance among directors has always
					influenced the portrayal of women in films. Her thoughts expand: Does the director’s
					gender affect the age of actresses, with female directors offering more opportunities for
					older women?
				</p>
				<Ages />
				<div class="flex flex-row items-center justify-center gap-4">
					<p class="bg-yellow-200 p-4 text-xl text-black">
						Regardless of the movie director’s gender, the peak age, where the highest number of
						actors.tresses is concentrated, is consistently lower for actresses compared to actors.
						Additionally, the age range for actresses appears more concentrated, or narrower, while
						the distribution for actors is broader, spanning a wider range of ages.
					</p>
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						To Madame, this trend suggests that female actresses face younger and stricter
						age-related preferences in casting decisions, regardless of whether the director is male
						or female. It may highlight the trend in the cinema industry only to represent
						relatively young women, and this can be related to their physical appearance or their
						secondary role as wives, mothers and lovers.
					</p>
				</div>

				<h2 class="mb-4 flex justify-start text-3xl font-bold text-black">... through Time ...</h2>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					She begins to explore historical trends, asking herself whether this disparity is a
					long-standing issue or a more recent development.
				</p>
				<DirectorsTime />
				<div class="flex flex-row items-center justify-center gap-4">
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						At first sight, Madame notices that the average female character proportion constantly
						stands at around 30 to 40%, all director gender combined. She now has evidence that
						gender distribution is a long-standing problem. However, she observes that female
						directors portray more women than male directors in their movies. As well, you can
						notice an interesting trend around the year 1938, where women were more represented in
						movies directed by men. “Would this be correlated in any way to war?” Madame wonders….
					</p>
				</div>
				<h2 class="mb-4 flex justify-start text-3xl font-bold text-black">
					... accross the World ...
				</h2>

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Then, she wonders which countries do the best job at representing women on screen.
					Perhaps, she thinks with a smile, she was born in the wrong time or place.
				</p>
				<div class="bg-yellow-200 p-4 text-xl text-black">
					<p>
						The analysis of female character representation, particularly of average female
						character proportion per movie, shows clear differences across countries and depending
						on the gender of the director. For male-directed films, the Philippines (42.4%), Mexico
						(40.9%), and Japan (40.5%) rank highest, while Russia (28.8%) and Denmark (29.6%) show
						the lowest proportions. Female-directed films fare best in Sweden, where nearly half of
						the characters are women, but countries like Denmark (34.8%), Japan, China, and India
						lag behind.
					</p>
					<p>
						Interestingly, Denmark consistently ranks among the worst for female representation,
						regardless of the director’s gender. Japan flips its position, ranking high in
						male-directed movies but falling behind for female-directed ones. If Madame wanted the
						best chances of starring in a film with strong female representation, she might have
						been better off in Sweden or the Philippines, far from Denmark’s dismal numbers.
					</p>
				</div>
				<h2 class="mb-4 flex justify-start text-3xl font-bold text-black">
					What about Movie Genres?
				</h2>

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Having explored the best times, places, and opportunities for actresses, Madame’s thoughts
					take a deeper turn. She finds herself wondering if there is a specific genre where women
					are most likely to be represented on screen. Could there be a particular category where
					her chances of landing a meaningful role are higher?
				</p>
				<div class="flex w-full flex-col"><Chart /></div>
				<h2 class="mb-4 flex justify-start text-2xl font-bold text-black">
					Top movie genres through time
				</h2>
				<p class="w-full border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame’s look into the top genres in films directed by men and women shows some
					interesting trends.
				</p>
				<div class="flex flex-row items-center justify-center gap-4">
					<p class=" bg-yellow-200 p-4 text-xl text-black">
						Drama is the number one genre for both men and women directors, though it’s a broad
						category that might affect how women are portrayed. Comedy and World Cinema show similar
						patterns across both genders, with women represented fairly equally.
					</p>
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						One possible explanation for these two observations is that cinematic genres such as
						Drama, Comedy, and World Cinema are broad categories that encompass a wide range of
						sub-genres. Hence, considering the way that these subgenres were clustered influences
						the genre distribution, and considering subgenres separately could lead to more varied
						portrayals of women within these genres.
					</p>
				</div>
				<div class="flex flex-row items-center justify-center gap-4">
					<p class=" bg-yellow-200 p-4 text-xl text-black">
						Romance is consistently in the top six for female-directed films, showing that women
						directors tend to focus on relationship-driven stories. Action was a top genre for
						female directors in the 1980s but shifts progressively, ending as the top four for male
						directors by 2011.
					</p>
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						To Madame, these results make sense: women directors seem to focus on
						relationship-driven stories. It’s no wonder her all-time favorite movies, like The
						Notebook or Notting Hill, are romantic classics. But then, something clicks: has her
						love for these stories been shaped by the very clichés she’s starting to question? Those
						love stories she’s dreamed of mostly define women by their relationships with men. And
						what about Action? It used to be a top genre for female directors, but over the years,
						it’s shifted to being more male-dominated. What does it say about the kinds of stories
						women are expected, or “allowed” by the film industry to tell?
					</p>
				</div>
				<div class="flex flex-row items-center justify-center gap-4">
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						At the same time, Madame looks at more “niche” genres, as well as the genres where there
						is the greatest gaps in female character representation between male and female-directed
						movies.
					</p>
					<p class=" bg-yellow-200 p-4 text-xl text-black">
						Western and War/Military genres show lower female representation, with female directors
						producing fewer films in these areas. Documentary films reveal a contrast, with
						female-directed documentaries increasing female representation by 37%, while
						male-directed films portray 25% fewer women.
					</p>
				</div>
				<h2 class="mb-4 flex justify-start text-3xl font-bold text-black">
					... but Movie Genres with high proportion of Female Characters?
				</h2>

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Then, after digging into the data about genres where women are portrayed the most, for
					both men and women-directed movies, she finds herself almost laughing at the answer. It’s
					not what she expected at all. Amused by the irony, she decides to send this little game to
					Miss, her childhood friend, also an actress, eager to see her reaction. She needs to
					classify the 3 genres below by the proportion of female characters, from the highest to
					the lowest.
				</p>
				<div class="flex flex-row gap-4">
					<GenresF />
					<GenresM />
				</div>
				<p class=" bg-yellow-200 p-4 text-xl text-black">
					Overall, while mainstream genres show similar female representation in both male- and
					female-directed films, niche genres reveal more significant differences. Female directors
					tend to portray more women in romance, while male directors dominate action genres. These
					findings suggest that while female directors strive for representation, they still face
					genre-driven limitations imposed by the film industry.
				</p>
				<div class="flex w-full">
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						Excited by her findings, Madame messages her friend Miss:
					</p>
				</div>

				<div class="flex w-full flex-col space-y-4 p-4">
					<!-- Left message (received) -->
					<div class="flex w-full justify-end">
						<div
							class="max-w-[80%] rounded-2xl rounded-tr-none bg-emerald-400 px-4 py-2 text-white"
						>
							<p class="text-md">Want to shoot a LGBT movie together?</p>
						</div>
					</div>

					<!-- Right message (sent) -->
					<div class="flex w-full">
						<div class="max-w-[80%] rounded-2xl rounded-tl-none bg-orange-400 px-4 py-2 text-white">
							<p class="text-md">Now that’s an interesting idea!</p>
						</div>
					</div>
					<div class="flex w-full">
						<div class="max-w-[80%] rounded-2xl rounded-tl-none bg-orange-400 px-4 py-2 text-white">
							<p class="text-md">
								But how will we be portrayed? I don’t want to be categorize into stereotypes. No
								more 'What do we do now?'. I'm tired "Brainless Beauty" role ...
							</p>
						</div>
					</div>
				</div>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					With this realization, Madame refocuses her efforts on understanding the deeper issue of
					female stereotypes in films. She decides to analyze tropes, the recurring themes and
					character archetypes commonly used in storytelling.
				</p>
			</div>

			<div
				class="flex flex-col items-center justify-center gap-4 p-9 text-justify"
				id="stereotypes"
			>
				<h2 class="mb-4 text-5xl font-bold text-black">Stereotropes</h2>
				<p class="bg-yellow-200 p-4 text-xl text-black">
					A trope is a recurring theme, motif, or character type in literature, film, and media that
					acts as a storytelling shortcut, helping audiences quickly grasp characters or situations
					while often perpetuating stereotypes.
				</p>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					For example, Madame had a Final Girl character as role in the movie: the sole survivor at
					the end of a movie when everyone else has perished. The same most represented trope in our
					dataset.
				</p>
				<div class="flex w-full flex-col">
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						To explore the prevalence of stereotypes in films, Madame analyzes the distribution of
						these tropes.
					</p>
				</div>

				<div
					class="border-1 flex flex-col items-center justify-center gap-4 border-orange-300 bg-origin-border"
				>
					<WordsM />
					<h2 class="mb-4 flex justify-start text-2xl font-bold text-black">
						Gendered Tropes' Distribution
					</h2>
				</div>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame is shocked! There are so few female tropes compared to the male ones! Could it be
					because women have very precise stereotypical roles?
				</p>
				<p class="bg-yellow-200 p-4 text-xl text-black">
					It appears the tropes known as feminine are quite often describing women either by their
					appearance (Beauty, Blonde, Classy) either by their intelligence, or Madame notices, even
					by their non-intelligence (Dumb, Brainless). Moreover, women are being passive in their
					tropes (Final girl, Broken bird) and are defined through others (the girl that does not
					die compared to the others, the girl that had her heart broken). Where men are defined as
					active through their job (cop, corporate) or their brilliant actions (swordman, hero).
				</p>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame now bet that those stereotypes were created by men to define women in narrow roles.
					She wonders whether female directors will challenge these clichés or inadvertently fall
					into their trap.
				</p>
				<Tvtropes />
				<p class="bg-yellow-200 p-4 text-xl text-black">
					As expected, female directors include more women in their films, where male directors
					really have the space to develop many men characters. However, they also rely on the same
					tropes as male directors. It seems these clichés are so deeply rooted that even women
					struggle to envision intelligent and powerful female characters beyond these stereotypes.
				</p>
			</div>
			<div
				class="flex flex-col items-center justify-center gap-4 p-9 text-justify"
				id="bechdeltest"
			>
				<div class="flex w-full flex-col space-y-4 p-4">
					<!-- Right message (sent) -->
					<div class="flex w-full justify-end">
						<div
							class="max-w-[80%] rounded-2xl rounded-tr-none bg-emerald-400 px-4 py-2 text-white"
						>
							<p class="text-md">
								Ugh, it’s so frustrating. Women in movies are way too stereotyped, even in films by
								women. And they’re always so passive!
							</p>
						</div>
					</div>
					<!-- Left message (received) -->
					<div class="flex w-full">
						<div class="max-w-[80%] rounded-2xl rounded-tl-none bg-orange-400 px-4 py-2 text-white">
							<p class="text-md">I get it… Ever heard of the Bechdel Test?</p>
						</div>
					</div>

					<div class="flex w-full justify-end">
						<div
							class="max-w-[80%] rounded-2xl rounded-tr-none bg-emerald-400 px-4 py-2 text-white"
						>
							<p class="text-md">
								It sounds familiar, but I can not remember the details. What is it?
							</p>
						</div>
					</div>
					<!-- Left message (received) -->
					<div class="flex w-full">
						<div class="max-w-[80%] rounded-2xl rounded-tl-none bg-orange-400 px-4 py-2 text-white">
							<p class="text-md">
								It’s simple: 1) The film must have at least two named female characters; 2) They
								must talk to each other; 3) Their conversation must be about something other than a
								man. Not many films pass!
							</p>
						</div>
					</div>
				</div>
				<h2 class="mb-4 text-5xl font-bold text-black">Bechdel Test</h2>

				<p class="bg-yellow-200 p-4 text-xl text-black">
					The Bechdel Test, created by cartoonist Alison Bechdel in her 1985 comic strip Dykes to
					Watch Out For, evaluates gender representation in films. While it doesn’t measure the
					quality of a film, it highlights whether women have meaningful roles beyond their
					relationships with men.
				</p>

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Intrigued, she wonders if her friend Miss’s nine favorite movies pass the test. Eager to
					find out, Madame checks them one by one, comparing whether they meet the criteria.
				</p>
				<MemoryGame />
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame then studies the proportion of male- and female-directed films that pass the
					Bechdel Test, clustering them into "BEST" (those that pass: 3/3) and "WORST" (those that
					don’t: 0/3, 1/3, 2/3). By analyzing these patterns, she hopes to uncover which directors
					are more likely to break away from stereotypical portrayals of women in cinema.
				</p>
				<BechdelRatings />

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					As Madame sifts through the data, the results start to reveal some intriguing patterns. It
					becomes clear that films directed by women tend to have a higher success rate in passing
					the Bechdel Test, with a notable proportion achieving the maximum score of 3. Furthermore,
					she almost laughs after noticing that the proportion of movies which score 1 to the test
					is higher than the one for a score of 2 : Would this mean that directors tend to not to
					represent any women rather than to make them talk in the movie ?
				</p>
				<BechdelCategory />

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					In order to dig deeper, Madame focuses on the emotional tones of movies, comparing both
					‘pass’ and ‘fail’ ones. She compares the emotional range of films with a fully successful
					Bechdel Test (score of 3), separated by whether the director is male or female.
				</p>
				<EmotionsBechdel />
				<p class="bg-yellow-200 p-4 text-xl text-black">
					Looking at emotional breadth between the two groups, we can notice that films directed by
					women actually seem to explore the same diverse array of emotions as films directed by
					men. However, the distribution highlights subtle variations: female-directed films display
					slightly higher intensities in emotions like joy and sadness, suggesting a heightened
					focus on emotionally resonant storytelling. Overall, the difference between passing and
					failing the bechdel is quite similar for both directors genders, especially regarding the
					anger and sadness emotions. The movies that pass have a tendency for sadness and on the
					opposite, movies that fail have a tendency for anger. The same observation is highlighted
					by the study conducted in “The Gender Stereotyping of Emotions.”
					<a
						href={'https://doi.org/10.1111/j.1471-6402.2000.tb01024.x'}
						class="text-center font-semibold text-black"
						target="_blank"
						>(Plant, E. A. 2006)
					</a>
				</p>
			</div>

			<div class="flex flex-col items-center justify-center gap-4 p-9 text-justify" id="success">
				<h2 class="mb-4 text-5xl font-bold text-black">Success</h2>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame’s phone vibrates. She grabs it, excited at the idea of receiving a new screenplay
					proposal. Ugh, the dreams of winning an Oscar vanish as she sees it’s a call from her
					landlord. “Shoot,” she mutters, “I’m short on rent again this month.” She wonders aloud,
					“Will I earn more money if I act in a movie that passes the Bechdel Test?”
				</p>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Surfing the web, she stumbles upon an article written by Johann Valentowitsch entitled: "<a
						href={'https://link.springer.com/article/10.1007/s11002-022-09652-5?.com'}
						class="text-center font-semibold text-black"
						target="_blank"
						>(Hollywood Caught in Two Worlds?)
					</a> The Impact of the Bechdel Test on the International Box Office Performance of Cinematic
					Films."
				</p>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					“Hollywood continues to rely heavily on male stereotypes for fear of losing international
					revenue,” the article states. “I knew it!” Madame exclaims. Her eyes dart across the
					screen. « on average […] films passing the test achieve significantly higher box office
					takings." Madame is thrilled, but the article lacks details regarding gender
					representation.
				</p>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Taking matters into her own hands, she grabs her computer and proceeds to further analyze
					her dataset.
				</p>
				<div class="flex flex-row gap-4">
					<p class="bg-yellow-200 p-4 text-xl text-black">
						After a closer look at director demographics, a striking tendency emerges: around 14,1%
						of movies passing the Bechdel test are directed by women whereas only 5% of the movies
						failing the Bechdel test have female directors.
					</p>
					<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
						« Obviously, this result is biased as the majority of director gender in my data set.
						But still, female directors tend to break gender stereotypes and create more meaningful
						interactions between female characters »."
					</p>
				</div>

				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Eager for more insights, Madame digs deeper into the dataset to explore financial success,
					by eliminating outliers to improve readability of the graph.
				</p>
				<div><Revenue /></div>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame did not expect such results. « Maybe Hollywood is not that different from the rest
					of the world after all », she thinks.
				</p>
				<p class="bg-yellow-200 p-4 text-xl text-black">
					Independently of the movie director gender, movies passing the Bechdel Test exhibit a
					broader and higher revenue range, on average slightly even more when directed by women.
					The difference is even stronger when focusing solely on women directors. As a latter of
					fact, meaningful interaction between women approximately increases the box office revenue
					from 27 to 47 million dollars.
				</p>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Madame’s attention then focused on a specific statement : « films with high production
					costs, gender balance is not a primary determinant of box office earnings ». « Mmmh,
					interesting » she thought. « Movie budget, that’s a parameter I had not considered yet.. »
				</p>
				<div><RatingsBoxOffice /></div>
				<p class="border-2 border-yellow-200 bg-origin-border p-4 text-xl italic text-black">
					Once again, the results of Madame’s analysis intrigue her. « Who knew there were such
					financial disparities amongst movie directors of different genders ? », she thought.
				</p>
				<p class="bg-yellow-200 p-4 text-xl text-black">
					Focusing on female directors, the average rating of a movie does not seem to correlate
					with the box office revenue. Women directors tend to earn little revenue, less than 200
					million, no matter the popularity of the movie. On the other hand, the range of box office
					revenue of movies directed by men seems to extend when better received by the critique.
					They are more often rewarded economically when appreciated by the critique as they can
					bring billions of dollars, but also have the most important financial means. In other
					words, movie budgets often exceed 200 million when directed by men whereas it barely
					reaches 80 million for the luckier movies directed by females.
				</p>
			</div>
		</div>
	</section>

	<section id="conclusion" class="h-min-screen relative flex flex-col items-center p-2">
		<h2 class="mb-12 text-5xl font-bold text-black">Conclusion</h2>
		<div class="flex w-3/4">
			<div class="w-full">
				<div class="my-4 h-px bg-orange-500"></div>
				{#each conclusionParts as part, index}
					<div
						class="transform transition-all duration-700 ease-out"
						class:opacity-0={!visibleSections[index]}
						class:translate-x-[-100%]={!visibleSections[index]}
						class:opacity-100={visibleSections[index]}
						class:translate-x-0={visibleSections[index]}
						class:animate-bounce={visibleSections[index]}
					>
						{#if index > 0}
							<div class="my-4 h-px bg-orange-400"></div>
						{/if}
						<p class="text-xl text-black">{part}</p>
					</div>
				{/each}
				<div class="my-4 h-px bg-orange-400"></div>
			</div>
		</div>
	</section>
	<!-- Our Team Section -->
	<section id="team" class="min-h bg-amber-200 py-8">
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
