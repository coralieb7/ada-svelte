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
	import List from '$lib/components/genres/List.svelte';
	import Tvtropes from '$lib/components/Tvtropes.svelte';

	let showBubbles = false;
	let navVisible = true;
	let lastScrollPosition = 0;
	let researchQuestionsVisible = [false, false, false];
	let visibleSections = [false, false, false];
	onMount(() => {
		const handleScroll = () => {
			const conclusionSection = document.querySelector('#conclusion');
			const introSection = document.querySelector('#intro');
			const navBar = document.querySelector('nav');
			const researchQuestionsSection = document.querySelector('#research-questions-datasets');
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

				if (currentScrollPosition > lastScrollPosition) {
					// Scrolling down
					navVisible = currentScrollPosition < 200; // Hide after scrolling down 100px
				} else {
					// Scrolling up
					navVisible = true;
				}

				lastScrollPosition = currentScrollPosition;

				// Apply navigation bar visibility
				if (navBar) {
					navBar.style.opacity = navVisible ? '1' : '0';
					navBar.style.visibility = navVisible ? 'visible' : 'hidden';
				}
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
		<h1 class="text-center text-6xl font-extrabold text-black sm:text-6xl lg:text-6xl">
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
	class={`fixed left-0 right-0 top-0 z-20 bg-transparent transition-all duration-300 ${navVisible ? 'visible opacity-100' : 'invisible opacity-0'}`}
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
				<a href="#datastory" class={`font-semibold text-black transition hover:text-pink-500`}
					>Datastory</a
				>
				<!-- Dropdown Menu -->
				<div
					class="w-30 absolute left-5 mt-2 hidden rounded-md bg-white shadow-lg group-hover:flex group-hover:flex-col"
				>
					<a
						href="#moviedirectors"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>Movie Directors</a
					>
					<a
						href="#femalerepresentation"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>Female</a
					>
					<a
						href="#bechdeltest"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>Bechdel Test</a
					>
					<a
						href="#tvtropes"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>Tv Tropes</a
					>
					<a
						href="#success"
						class="block px-4 py-2 text-sm text-gray-700 hover:bg-pink-100 hover:text-pink-500"
						>Success</a
					>
				</div>
			</div>
			<a href="#conclusion" class={`font-semibold text-black transition hover:text-violet-500`}
				>Conclusion</a
			>
			<a href="#team" class={`font-semibold text-black transition hover:text-rose-500`}>Our Team</a>
		</div>
	</nav>
</div>

<!-- Content Sections (below the large title) -->
<div class="space-y-20 bg-white p-6">
	<section id="intro" class="relative flex min-h-screen justify-center">
		<h2 class="mb-4 text-5xl font-bold text-black">INTRODUCTION</h2>
		<!-- First Bubble -->
		<div
			class="bubble-container-left absolute flex items-center justify-center"
			class:visible={showBubbles}
		>
			<div class="bubble-content">
				<p class="leading-relaxed text-black">
					Meet Madame. <br /> Sitting at her table, she is<br /> holding her very first movie
					script, a huge<br />
					opportunity she’s dreamed about for years. Suddenly,<br /> as she flips through the pages,
					one line catches her eye:<br /> “WHAT DO WE DO NOW?” Why would this easy as pie
					<br />question disturb her so much? Because she delivers it <br />to a man in a moment of
					high tension, waiting for him to <br />decide the next move. Disillusioned, Madame
					wonders: <br />Is this really how it starts? A character with little to <br />say, caught
					in a moment of indecision, as <br />usual, relying on a man to <br />take charge?
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
					This iconic line is <br />more than just dialogue. It’s a <br />symbol of a deeper issue:
					women in films<br />
					are often underrepresented and stereotyped,<br /> their roles shaped by limited
					perspectives.<br /> “What Do We Do Now?”<br /> isn’t just the title of our project—it’s a
					question<br />
					we are asking to explore how the gender of<br /> a movie director influences how <br />
					women are portrayed <br />on screen.
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
					Through our analysis,<br /> we’ll explore how the gender of a <br />director influences
					female representation,<br /> uncover the stereotypes that still dominate, and <br />track
					how women’s roles have evolved across<br /> time and cultures. Because some questions<br
					/>
					raised in cinema do not always stay on screen:<br /> they reflect real-world dynamics,
					mirroring <br />how groups of people and behaviors are <br />portrayed in our society.
				</p>
			</div>
		</div>
	</section>

	<!-- Research Questions Section-->
	<section
		id="research-questions-datasets"
		class="relative flex flex-col items-center justify-center"
	>
		<div class="flex min-h-screen flex-col items-center justify-start gap-16">
			<div class="flex w-3/4 flex-col items-center gap-10">
				<h2 class="mb-4 text-5xl font-bold text-black">RESEARCH QUESTIONS</h2>

				<div class="w-full">
					<div class="my-4 h-px bg-black"></div>
					{#each ['How does the gender of a movie director influence the portrayal of women in cinema?', 'What are the key female stereotypes in movies?', "How have women's roles evolved over time and across cultures?"] as question, index}
						<div
							class="transform transition-all duration-700 ease-out"
							class:opacity-0={!researchQuestionsVisible[index]}
							class:translate-x-[-100%]={!researchQuestionsVisible[index]}
							class:opacity-100={researchQuestionsVisible[index]}
							class:translate-x-0={researchQuestionsVisible[index]}
						>
							{#if index > 0}
								<div class="my-4 h-px bg-black"></div>
							{/if}
							<p class="text-xl text-black">{question}</p>
						</div>
					{/each}
					<div class="my-4 h-px bg-black"></div>
				</div>
			</div>
			<div class="flex flex-col items-center justify-center gap-10 space-x-4">
				<h2 class="relative mb-4 text-5xl font-bold text-black">DATASETS</h2>
				<div class="flex items-center justify-center space-x-4">
					{#each circleData as circle, index}
						<div
							role="button"
							tabindex="0"
							class="relative flex h-48 w-48 items-center justify-center rounded-full border-2 border-black transition-all duration-300"
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
				<p class=" text-5xl font-bold">DATASTORY</p>
			</div>

			<div
				class="flex flex-col items-center justify-center gap-4 p-8 text-justify"
				id="moviedirectors"
			>
				<h2 class="mb-4 flex justify-start text-3xl font-bold text-black">Movie Directors</h2>
				<div class="flex flex-row gap-4">
					<div
						class="flex h-64 w-80 border border-black bg-cover"
						style="background-image: url('/img/dir_distribution.jpeg');"
					></div>
					<div
						class="flex h-64 w-80 border border-black bg-cover"
						style="background-image: url('/img/char_distribution.jpeg');"
					></div>
				</div>
				<p class="text-black">
					It doesn't take long for the first revelation to appear, stark and undeniable: the gender
					distribution among film directors is far from balanced. What's more, the gender
					distribution of the movie directors - 90% male, 10% female - is far more contrasted than
					that of the actors: 67% of the actors are male, while the remaining 33% are female.
				</p>
			</div>

			<div
				class="flex flex-col items-center justify-center gap-4 p-8 text-justify"
				id="femalerepresentation"
			>
				<h2 class="mb-4 text-3xl font-bold text-black">Female representation in Movies</h2>
				<p class="text-black">
					Madame’s curiosity grows as she wonders if the gender imbalance among directors has always
					influenced the portrayal of women in films. She begins to explore historical trends,
					asking herself whether this disparity is a long-standing issue or a more recent
					development. As she digs deeper, she recalls the idea of the "celluloid ceiling"—an
					invisible but powerful barrier that has kept women from reaching key creative roles in
					filmmaking for decades.
				</p>
				<Ages />
				<p class="text-black">
					Her thoughts expand: Does the director’s gender affect the age of actresses, with female
					directors offering more opportunities for older women?
				</p>
				<DirectorsTime />
				<p class="text-black">
					Regardless of the movie director’s gender, the peak age, where the highest number of
					actors. tresses is concentrated, is consistently lower for actresses compared to actors.
					Additionally, the age range for actresses appears more concentrated, or narrower, while
					the distribution for actors is broader, spanning a wider range of ages. To Madame, this
					trend suggests that female actors face stricter age-related preferences in casting
					decisions, regardless of whether the director is male or female. It highlights the
					persistent disparities in age representation between male and female actors within the
					film industry.
				</p>
				<p class="text-black">
					She also questions whether certain genres are more inclusive of women. Finally, she
					wonders which countries do the best job of representing women on screen. Perhaps, she
					thinks with a smile, she was born in the wrong time or place.
				</p>
				<div class="flex w-4/5 flex-col"><Chart /> <Chart /></div>
				<p class="text-black">Looking at the results, Madame finds that:</p>
				<p class="text-black">
					Having explored the best times, places, and opportunities for actresses, Madame’s thoughts
					take a deeper turn. She finds herself wondering if there is a specific genre where women
					are most likely to be represented on screen. Could there be a particular category where
					her chances of landing a meaningful role are higher?
				</p>
				<p class="text-black">
					DANS UNE BULLE NUAGE Our 35-year-old actress has always dreamed of living in a romance
					movie, like her all-time favorites The Notebook or Notting Hill. She’s always loved the
					idea of chance encounters, sweeping love stories, and those big, emotional moments. But as
					she thinks about the genres that would potentially focus most on women, something clicks:
					her own dreams and tastes might have been shaped by clichés. Indeed, those romantic ideals
					she’s held onto come from stories where women are mostly defined by their relationships
					with men. It’s a weird feeling, realizing that even her own dreams might be tied to the
					same stereotypes she’s so tired of seeing in society.
				</p>
				<p class="text-black">
					After digging into the data, she finds herself almost laughing at the answer. It’s not
					what she expected at all. Amused by the irony, she decides to send this little riddle to
					Miss, her childhood friend, also an actress, eager to see her reaction.
				</p>
				<List />
			</div>
			<div
				class="flex flex-col items-center justify-center gap-4 p-9 text-justify"
				id="bechdeltest"
			>
				<h2 class="mb-4 text-3xl font-bold text-black">Bechdel Test</h2>

				<p class="text-black">
					After a moment of considering the surprising data, Miss replies with a laugh,
				</p>
				<div
					class="flex h-80 w-32 border border-black bg-cover"
					style="background-image: url('/img/sms.jpg');"
				></div>
				<!-- IMAGE DON'T SHOW -->
				<p class="text-black">
					Intrigued, she wonders if her friend Miss’s three favorite movies pass the test. Eager to
					find out, Madame checks them one by one, comparing whether they meet the criteria.
				</p>
				<p class="text-black">JEU A FAIRE</p>
				<p class="text-black">
					Excited by this discovery, Madame decided to dive deeper into the data. She starts by
					exploring which films pass the test.
				</p>
				<BechdelRatings />
				<p class="text-black">
					She quickly uncovers some key results: films directed by women tend to pass the Bechdel
					Test more often than those directed by men.
				</p>
				<p class="text-black">
					Next, she selects all the films that pass the Bechdel Test (score of 3) and begins
					analyzing the correlation. PARLER MODELE ML POUR PRÉDIRE LE SCORE DU TEST D’UN FILM AVEC
					LES INFOS QU’ON A
				</p>
				<EmotionsBechdel />
				<p class="text-black">
					As Madame sifts through the data, the results start to reveal some interesting patterns.
					It becomes clear that films directed by women tend to have ?, and these films also show ?.
					Eager to dig deeper, Madame then focuses on the emotional tones of these Bechdel-passing
					films. She compares the emotional range of films with a fully successful Bechdel Test
					(score of 3), separated by whether the director is male or female. Looking at emotional
					breadth between the two groups, she notices that films directed by women actually seem to
					explore the same array of emotions as the one of films directed by men. Madame is now more
					convinced that the director's gender plays a significant role not just in the inclusion of
					women in film but also in shaping the emotional richness of their stories.
				</p>
			</div>
			<div class="flex flex-col items-center justify-center gap-4 p-9 text-justify" id="tvtropes">
				<h2 class="mb-4 text-4xl font-bold text-black">TV Tropes</h2>
				<p class="text-black">
					But a question remains: what if the stereotypes weren’t just influenced by the director's
					gender, but were more deeply rooted in societal structures? Madame starts to consider the
					possibility that these recurring patterns might be shaped by broader cultural norms, not
					just the people behind the camera. To explore this further, she turns to TV Tropes, a
					collection of common themes and character types seen across television and film. After
					examining the gender ratio associated with various tropes over a range of X movies, she is
					able to link these stereotypes to the representation of women. The data reveals that :
				</p>
				<Tvtropes />
				<p class="text-black">
					To dig deeper, Madame filters the results by the gender ratio of directors, exploring
					whether certain tropes are more common in films directed by women. She also looks at the
					balance between female and male characters in these films in order to visualize how women
					are represented across different tropes. Les hommes représentent plus les clichés d’hommes
					que ceux des femmes (ils s’en foutent tellement des femmes qu’ils ne les représentent même
					pas) Les femmes représentent des femmes clichés ; elles sont contraintes de jouer avec les
					stéréotypes !!! Certains TV tropes stand out: 20 mec vs 100 meufs pour Classy Cat-burglar,
					hors tv tropes que utilisé par des movie directeur hommes → Ils utilisent des clichés :
					Les femmes sont vues comme pernicieuses, gold digger, Now, Madame begins to wonder: could
					these stereotypes be linked to broader societal norms, or are they merely a reflection of
					industry trends?
				</p>
			</div>
			<div class="flex flex-col items-center justify-center gap-4 p-9 text-justify" id="success">
				<h2 class="mb-4 text-4xl font-bold text-black">Success</h2>
				<p class="text-black">
					With all the data and insights she’s gathered, Madame now has one word echoing in her
					head: success. Madame has long struggled in the artistic world, finding it difficult to
					land good roles and achieve recognition and audience validation. She starts to explore how
					industry trends affect the box office and public reception of films, using the IMDb
					Ratings and TMDB Ratings datasets. and success metrics.
				</p>
				<div class="flex max-w-6xl">
					<div class="flex flex-row items-center justify-center -space-x-20">
						<!-- First flex container takes 2/3 of the screen width -->
						<div><AverageRatingsOpti /></div>
						<div><AverageRatingsWorst /></div>
					</div>
				</div>
				<p class="text-justify text-black">
					She narrows her focus to two groups of films: those that pass the Bechdel Test with strong
					female representation and those that fail with poor female representation. To do so, she
					creates two categories of films based on specific conditions. The first group includes
					movies that pass the Bechdel Test and have significant female representation among the
					cast (over 35%), which she labels "wonderful". The second group consists of films that
					fail the Bechdel Test (score of 2 or less) and have poor female representation (35% or
					less), which she labels "horrible."
				</p>
				

				<RendementsOpti />
				<RendementsWorst />
				<p class="text-black">The results show that [...]</p>
			</div>
		</div>
	</section>

	<section id="conclusion" class="h-min-screen relative flex flex-col items-center p-9">
		<h2 class="mb-12 text-5xl font-bold text-black">Conclusion</h2>
		<div class="flex w-3/4">
			<div class="w-full">
				<div class="my-4 h-px bg-black"></div>
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
							<div class="my-4 h-px bg-black"></div>
						{/if}
						<p class="text-xl text-black">{part}</p>
					</div>
				{/each}
				<div class="my-4 h-px bg-black"></div>
			</div>
		</div>
	</section>
	<!-- Our Team Section -->
	<section id="team" class="min-h bg-amber-100 py-8">
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
