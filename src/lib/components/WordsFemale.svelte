<script>
	let activeWord = null;

	const words = [
		{
			text: 'FinalGirl',
			info: 'The almost-Always Female last survivor of a Slasher Movie.',
			percentage: 8.11,
			offset: 'ml-0'
		},
		{
			text: 'BrokenBird',
			info: 'A sympathetic character becomes stoic, cynical, aggressive and/or badass to cope with emotional trauma.',
			percentage: 3.63,
			offset: 'ml-1'
		},
		{
			text: 'DumbBlonde',
			info: "Someone (usually a woman) who's blonde and unintelligent.",
			percentage: 4.58,
			offset: 'ml-4'
		},
		{
			text: 'BrainlessBeauty',
			info: "Someone who's attractive and unintelligent.",
			percentage: 2.77,
			offset: 'ml-3'
		},
		{
			text: 'ValleyGirl',
			info: 'Girls (usually teenagers) who are more concerned with fashion and trends than any kind of intelligence, sophistication or anything relating to common-sense.',
			percentage: 1.24,
			offset: 'ml-6'
		},
		{
			text: 'ClassyCatBurglar',
			info: 'A skilled, sexy, mysterious female thief, who is just as agile and elegant as a cat.',
			percentage: 0.48,
			offset: 'ml-1'
		}
	];
	// Function to calculate font size based on percentage
	function getFontSize(percentage) {
		// Base size is 1rem (16px), max size is 3rem (48px)
		const minSize = 1;
		const maxSize = 20;
		const scale = (percentage - 0) / (100 - 0); // normalize percentage to 0-1
		const size = minSize + (maxSize - minSize) * scale;
		return `${size}rem`;
	}
</script>

<div class="relative p-8">
	{#each words as word, index}
		<div class="relative my-1">
			<div
				role="button"
				tabindex="0"
				class={`cursor-pointer font-semibold text-violet-300 transition-colors hover:text-violet-500 ${word.offset}`}
				style="font-size: {getFontSize(word.percentage)};"
				on:mouseenter={() => (activeWord = index)}
				on:mouseleave={() => (activeWord = null)}
			>
				{word.text}

				{#if activeWord === index}
					<div
						class="absolute right-full top-0 ml-4 w-64 rounded-lg bg-white p-4 text-base shadow-lg"
					>
						<div class="text-left text-lg font-bold text-violet-800">{word.text}</div>
						<div class="mt-2 text-left text-violet-600">{word.info}</div>
						<div class="mt-2 text-left font-semibold text-violet-700">{word.percentage}%</div>
					</div>
				{/if}
			</div>
		</div>
	{/each}
</div>
