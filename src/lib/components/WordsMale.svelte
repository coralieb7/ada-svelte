<script>
	let activeWord = null;

	const words1 = [
		{
			text: 'DirtyCop',
			info: 'A cop who engages in police misconduct or is straight-up evil.',
			percentage: 7.25,
			offset: 'ml-12',
			genres: 'Thriller, Crime and Mystery, Drama'
		},

		{
			text: 'JerkJock',
			info: 'Popular asshole bully in a Varsity jacket.',
			percentage: 3.91,
			offset: 'ml-3',
			genres: 'Comedy, Adventure, Drama'
		},
		{
			text: 'BruiserWithASoftCenter',
			info: 'Tough characters are capable of having soft hearts.',
			percentage: 0.38,
			offset: '-ml-12',
			genres: "Family's Films, Animation, Action"
		},
		{
			text: 'TranquilFury',
			info: 'Calm, but serious and violently angry.',
			percentage: 3.81,
			offset: 'ml-1',
			genres: 'Drama, Thriller, Action'
		},

		{
			text: 'YoungGun',
			info: 'Gun-toting kid.',
			percentage: 1.34,
			offset: '-ml-6',
			genres: 'Western, Adventure, Crime and Mystery'
		},
		{
			text: 'JunkieProphet',
			info: 'Drug-induced future sight.',
			percentage: 0.38,
			offset: 'ml-2',
			genres: 'Action, Thriller, Science Fiction'
		},
		{
			text: 'SurferDude',
			info: 'Stereotypical surfer character, bro.',
			percentage: 1.34,
			offset: '-ml-9',
			genres: 'Comedy, Drama, Romance'
		},
		{
			text: 'HenpeckedHusband',
			info: 'The woman in the relationship calls the shots.',
			percentage: 3.05,
			offset: '-ml-3',
			genres: 'Comedy, Drama, Romance'
		},
		{
			text: 'ByronicHero',
			info: 'A troubled, brooding, sometimes selfish outcast who strives for an unattainable (or what they perceive as an unattainable) goal, which often causes drama.',
			percentage: 2.19,
			offset: 'ml-8',
			genres: 'Drama, Adventure, Action'
		},

		{
			text: 'StupidCrooks',
			info: "Idiots who can't even commit a crime right.",
			percentage: 2.1,
			offset: 'ml-5',
			genres: 'Crime and Mystery, Comedy, Drama'
		},
		{
			text: 'CulturedBadass',
			info: "A badass who's also very sophisticated and enjoys the finer things in life.",
			percentage: 2,
			offset: 'ml-6',
			genres: 'Drama, Action, Adventure'
		},
		{
			text: 'DumbMuscle',
			info: 'Plenty of brawn and/or fighting skill, but lacking on brains and/or common sense.',
			percentage: 1.9,
			offset: 'ml-2',
			genres: 'Comedy, Adventure, Action'
		},
		{
			text: 'GadgeteerGenius',
			info: 'Character is good at inventing gadgets and other devices.',
			percentage: 1.81,
			offset: 'ml-0',
			genres: 'Adventure, Action, Science Fiction'
		}
	];
	const words2 = [
		{
			text: 'MasterSwordman',
			info: 'A character noted for their mastery of the sword.',
			percentage: 1.81,
			offset: 'ml-12',
			genres: 'Adventure, Action, Drama'
		},
		{
			text: 'SelfMadeMan',
			info: 'Everything this character has, they earned it the hard way, despite humble beginnings.',
			percentage: 1.81,
			offset: '-ml-6',
			genres: 'Comedy, Drama, Romance'
		},
		{
			text: 'DeanBitterman',
			info: 'The stereotypical nasty school principal.',
			percentage: 1.81,
			offset: '-ml-12',
			genres: "Comedy, Family's Films, Drama"
		},
		{
			text: 'HitmanWithAHeart',
			info: 'Even a callous assassin has standards.',
			percentage: 1.72,
			offset: 'ml-10',
			genres: 'Crime and Mystery, Thriller, Adventure'
		},
		{
			text: 'Revenge',
			info: 'Getting retribution on the one who wronged you.',
			percentage: 1.72,
			offset: 'ml-9',
			genres: 'Drama, Adventure, Thriller'
		},

		{
			text: 'BountyHunter',
			info: 'A private contractor rewarded by the authorities for killing or capturing those wanted by the law.',
			percentage: 1.34,
			offset: 'ml-1',
			genres: 'Comedy, Crime and Mystery, Adventure'
		},
		{
			text: 'MorallyBankruptBanker',
			info: 'An evil banker.',
			percentage: 0.76,
			offset: '-ml-6',
			genres: 'Drama, Comedy, Adventure'
		},
		{
			text: 'EccentricMentor',
			info: 'A mentor who is quirky, yet still wise and skilled.',
			percentage: 0.67,
			offset: '-ml-10',
			genres: 'Adventure, Drama, Comedy'
		},
		{
			text: 'GentlemenThief',
			info: 'A Man of Wealth and Taste who steals for sport.',
			percentage: 1.34,
			offset: '-ml-3',
			genres: 'Crime and Mystery, Action, Adventure'
		},
		{
			text: 'OfficerAndAGentleman',
			info: 'A cultured, refined, polite, and honorable military officeholder.',
			percentage: 1.34,
			offset: 'ml-6',
			genres: 'Adventure, Action, Science Fiction'
		},
		{
			text: 'ChildProdigy',
			info: "A genius who's anywhere between 3-12 years old.",
			percentage: 1.24,
			offset: 'ml-7',
			genres: "Drama, Family's Films, Comedy"
		},
		{
			text: 'AbsentMindedProfessor',
			info: 'A scientist who is often lost in thought and a little out of touch with the world around them.',
			percentage: 1.24,
			offset: 'ml-2',
			genres: 'Science Fiction, Adventure, Thriller'
		},
		{
			text: 'CrazySurvivalist',
			info: 'Has prepared for the worst scenario and is also completely nuts and/or a total asshole to others.',
			percentage: 1.05,
			offset: '-ml-3',
			genres: 'Adventure, Action, Thriller'
		},
		{
			text: 'FatherToHisMen',
			info: 'This commander really cares about their followers.',
			percentage: 0.95,
			offset: '-ml-2',
			genres: 'Adventure, War and Military, Drama'
		},

		{
			text: 'EgomaniacHunter',
			info: 'He hunts the rarest, most exotic, most dangerous game, just to prove that he can.',
			percentage: 0.95,
			offset: 'ml-12',
			genres: "Adventure, Family's Films, Fantasy"
		},
		{
			text: 'ConsumateProfessional',
			info: 'All about the job, and nothing but the job.',
			percentage: 0.95,
			offset: 'ml-3',
			genres: 'Comedy, Crime and Mystery, Drama'
		},

		{
			text: 'RomanticRunnerup',
			info: 'The third wheel of the Love Triangle.',
			percentage: 0.95,
			offset: 'ml-0',
			genres: 'Comedy, Drama, Fantasy'
		},
		{
			text: 'WarriorPoet',
			info: 'One trained in the ways of both art and war.',
			percentage: 0.95,
			offset: 'ml-3',
			genres: 'Adventure, Drama, Action'
		},
		{
			text: 'LoveableRogue',
			info: 'They break the law at least somewhat for their own gain, but are charming and affable enough for the audience to root for them.',
			percentage: 0.76,
			offset: '-ml-6',
			genres: 'Comedy, Adventure, Drama'
		},

		{
			text: 'LoserProtagonist',
			info: "Society's standards consider this protagonist a loser.",
			percentage: 0.67,
			offset: '-ml-8',
			genres: 'Comedy, Drama, Action'
		},
		{
			text: 'RetiredOutlaw',
			info: "An Outlaw who is trying to add 'former' to his description.",
			percentage: 0.67,
			offset: 'ml-6',
			genres: 'Drama, Western, Adventure'
		},
		{
			text: 'HeartbrokenBadass',
			info: 'A very angsty badass who is emotionally broken after somebody dies who they personally love or care about.',
			percentage: 0.67,
			offset: 'ml-0',
			genres: 'Adventure, Action, Drama'
		},
		{
			text: 'FastestGunInTheWest',
			info: 'A character acknowledged in-universe to be a master of the Quick Draw.',
			percentage: 0.67,
			offset: '-ml-3',
			genres: 'Western, Adventure, Drama'
		},
		{
			text: 'AdventureArchaeologist',
			info: 'Archaeology portrayed as less scientific method, more adventure.',
			percentage: 0.67,
			offset: 'ml-0',
			genres: ' Adventure, Action, Thriller'
		},
		{
			text: 'BromanticFoil',
			info: 'A Foil to the male romantic lead.',
			percentage: 0.67,
			offset: 'ml-16',
			genres: 'Comedy, Drama, Romance'
		},
		{
			text: 'PlayfulHacker',
			info: 'A character who hacks computers for fun.',
			percentage: 0.57,
			offset: 'ml-12',
			genres: 'Adventure, Thriller, Action'
		},
		{
			text: 'GrumpyOldMan',
			info: 'A grouchy elder.',
			percentage: 2.19,
			offset: 'ml-3',
			genres: 'Drama, Comedy, World Cinema'
		},
		{
			text: 'EvilPrince',
			info: 'An ambitious prince(ss) usurps the throne by killing whoever is in the line of succession before them.',
			percentage: 0.48,
			offset: '-ml-20',
			genres: 'Adventure, Fantasy, Drama'
		},
		{
			text: 'HardboiledDetective',
			info: 'Stereotypical tough, cynical, hard-drinking Private Detective.',
			percentage: 0.48,
			offset: '-ml-18',
			genres: 'Horror, Crime and Mystery, Drama'
		},
		{
			text: 'CrazyJealousGuy',
			info: "'Get your hands off MY girl!'",
			percentage: 3.34,
			offset: 'ml-6',
			genres: 'Drama, Thriller, Comedy'
		},
		{
			text: 'ArrogantKungFuGuy',
			info: 'Their power and skill is only paralleled by a lack of social discipline and a lot of ego to go with it.',
			percentage: 0.38,
			offset: 'ml-0',
			genres: 'Action, Drama, Adventure'
		},
		{
			text: 'PsychoForHire',
			info: 'Loves torturing and murdering others, and getting paid for it.',
			percentage: 5.63,
			offset: 'ml-4',
			genres: 'Thriller, Action, Adventure'
		},

		{
			text: 'BigManOnCampus',
			info: 'The high school/college version of The Ace, admired by everyone (or nearly everyone).',
			percentage: 0.29,
			offset: 'ml-2',
			genres: 'Drama, Comedy, LGBT'
		},
		{
			text: 'CorruptCorporateExecutive',
			info: 'A villain who runs a corporation.',
			percentage: 6.97,
			offset: '-ml-24',
			genres: 'Adventure, Thriller, Drama'
		}
	];
	const words3 = [
		{
			text: 'FinalGirl',
			info: 'The almost-Always Female last survivor of a Slasher Movie.',
			percentage: 8.11,
			offset: 'ml-0',
			genres: 'Horror, Thriller, Comedy'
		},
		{
			text: 'BrokenBird',
			info: 'A sympathetic character becomes stoic, cynical, aggressive and/or badass to cope with emotional trauma.',
			percentage: 3.63,
			offset: 'ml-1',
			genres: 'Drama, Thriller, Comedy'
		},
		{
			text: 'DumbBlonde',
			info: "Someone (usually a woman) who's blonde and unintelligent.",
			percentage: 4.58,
			offset: 'ml-4',
			genres: 'Comedy, Romance, Adventure'
		}
	];
	const words4 = [
		{
			text: 'ValleyGirl',
			info: 'Girls (usually teenagers) who are more concerned with fashion and trends than any kind of intelligence, sophistication or anything relating to common-sense.',
			percentage: 1.24,
			offset: 'ml-6',
			genres: 'Comedy, Romance, LGBT'
		},
		{
			text: 'ClassyCatBurglar',
			info: 'A skilled, sexy, mysterious female thief, who is just as agile and elegant as a cat.',
			percentage: 0.48,
			offset: 'ml-1',
			genres: 'Thriller, Romance, Horror'
		}
	];
	const words5 = [
		{
			text: 'BrainlessBeauty',
			info: "Someone who's attractive and unintelligent.",
			percentage: 2.77,
			offset: 'ml-3',
			genres: 'Comedy, Drama, Romance'
		}
	];

	// Function to calculate font size based on percentage
	function getFontSize(percentage) {
		const minSize = 1;
		const maxSize = 20;
		const scale = (percentage - 0) / (100 - 0);
		const size = minSize + (maxSize - minSize) * scale;
		return `${size}rem`;
	}
</script>

<div class="relative p-8">
	<div class="grid grid-cols-3 -space-y-2">
		{#each words5 as word, index}
			<div class="relative my-1">
				<div
					role="button"
					tabindex="0"
					class={`cursor-pointer font-semibold text-violet-300 transition-colors hover:text-violet-500 ${word.offset}`}
					style="font-size: {getFontSize(word.percentage)};"
					on:mouseenter={() => (activeWord = `col5-${index}`)}
					on:mouseleave={() => (activeWord = null)}
				>
					{word.text}

					{#if activeWord === `col5-${index}`}
						<div
							class="absolute left-full top-0 z-50 ml-4 w-64 rounded-lg bg-white p-4 text-base shadow-lg"
						>
							<div class="text-left text-lg font-bold text-violet-800">{word.text}</div>
							<div class="mt-2 text-left text-violet-600">{word.info}</div>
              <div class="mt-2 text-left text-violet-600 italic">Top-3 Genres: {word.genres}</div>
							<div class="mt-2 text-left font-semibold text-violet-700">{word.percentage}%</div>
						</div>
					{/if}
				</div>
			</div>
		{/each}
		{#each words1 as word, index}
			<div class="relative">
				<div
					role="button"
					tabindex="0"
					class={`cursor-pointer font-semibold text-green-300 transition-colors hover:text-green-500 ${word.offset}`}
					style="font-size: {getFontSize(word.percentage)};"
					on:mouseenter={() => (activeWord = `col1-${index}`)}
					on:mouseleave={() => (activeWord = null)}
				>
					{word.text}

					{#if activeWord === `col1-${index}`}
						<div
							class="absolute left-full top-0 z-50 ml-4 w-64 rounded-lg bg-white p-4 text-base shadow-lg"
						>
							<div class="text-left text-lg font-bold text-green-800">{word.text}</div>
							<div class="mt-2 text-left text-green-600">{word.info}</div>
              <div class="mt-2 text-left text-green-600 italic">Top-3 Genres: {word.genres}</div>
							<div class="mt-2 text-left font-semibold text-green-700">{word.percentage}%</div>
						</div>
					{/if}
				</div>
			</div>
		{/each}
		{#each words3 as word, index}
			<div class="relative my-1">
				<div
					role="button"
					tabindex="0"
					class={`cursor-pointer font-semibold text-violet-300 transition-colors hover:text-violet-500 ${word.offset}`}
					style="font-size: {getFontSize(word.percentage)};"
					on:mouseenter={() => (activeWord = `col3-${index}`)}
					on:mouseleave={() => (activeWord = null)}
				>
					{word.text}

					{#if activeWord === `col3-${index}`}
						<div
							class="absolute left-full top-0 z-50 ml-4 w-64 rounded-lg bg-white p-4 text-base shadow-lg"
						>
							<div class="text-left text-lg font-bold text-violet-800">{word.text}</div>
							<div class="mt-2 text-left text-violet-600">{word.info}</div>
              <div class="mt-2 text-left text-violet-600 italic">Top-3 Genres: {word.genres}</div>
							<div class="mt-2 text-left font-semibold text-violet-700">{word.percentage}%</div>
						</div>
					{/if}
				</div>
			</div>
		{/each}
		{#each words2 as word, index}
			<div class="relative -space-y-4">
				<div
					role="button"
					tabindex="0"
					class={`cursor-pointer font-semibold text-green-300 transition-colors hover:text-green-500 ${word.offset}`}
					style="font-size: {getFontSize(word.percentage)};"
					on:mouseenter={() => (activeWord = `col2-${index}`)}
					on:mouseleave={() => (activeWord = null)}
				>
					{word.text}

					{#if activeWord === `col2-${index}`}
						<div
							class="absolute left-full top-0 z-50 ml-4 w-64 rounded-lg bg-white p-4 text-base shadow-lg"
						>
							<div class="text-left text-lg font-bold text-green-800">{word.text}</div>
							<div class="mt-2 text-left text-green-600">{word.info}</div>
              <div class="mt-2 text-left text-green-600 italic">Top-3 Genres: {word.genres}</div>
							<div class="mt-2 text-left font-semibold text-green-700">{word.percentage}%</div>
						</div>
					{/if}
				</div>
			</div>
		{/each}
		{#each words4 as word, index}
			<div class="relative my-1">
				<div
					role="button"
					tabindex="0"
					class={`cursor-pointer font-semibold text-violet-300 transition-colors hover:text-violet-500 ${word.offset}`}
					style="font-size: {getFontSize(word.percentage)};"
					on:mouseenter={() => (activeWord = `col4-${index}`)}
					on:mouseleave={() => (activeWord = null)}
				>
					{word.text}

					{#if activeWord === `col4-${index}`}
						<div
							class="absolute left-full top-0 z-50 ml-4 w-64 rounded-lg bg-white p-4 text-base shadow-lg"
						>
							<div class="text-left text-lg font-bold text-violet-800">{word.text}</div>
							<div class="mt-2 text-left text-violet-600">{word.info}</div>
              <div class="mt-2 text-left text-violet-600 italic">Top-3 Genres: {word.genres}</div>
							<div class="mt-2 text-left font-semibold text-violet-700">{word.percentage}%</div>
						</div>
					{/if}
				</div>
			</div>
		{/each}
	</div>
</div>
