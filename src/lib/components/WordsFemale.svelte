<script>
	let activeWord = null;

	const words = [
		{
			text: 'FinalGirl',
			info: 'Common stereotype in films',
			percentage: 23,
			offset: 'ml-0'
		},
		{
			text: 'BrokenBird',
			info: 'Horror movie survivor trope',
			percentage: 21,
			offset: 'ml-8'
		},
		{
			text: 'DumbBlonde',
			info: 'Supernatural romantic interest',
			percentage: 19,
			offset: 'ml-4'
		},
		{
			text: 'BrainlessBeauty',
			info: 'Female action hero',
			percentage: 15,
			offset: 'ml-12'
		},
		{
			text: 'ValleyGirl',
			info: 'Needs to be rescued',
			percentage: 9,
			offset: 'ml-6'
		},
		{
			text: 'ClassyCatBurglar',
			info: 'Needs to be rescued',
			percentage: 8,
			offset: 'ml-6'
		}
	];
	// Function to calculate font size based on percentage
	function getFontSize(percentage) {
		// Base size is 1rem (16px), max size is 3rem (48px)
		const minSize = 1;
		const maxSize = 3;
		const scale = (percentage - 0) / (100 - 0); // normalize percentage to 0-1
		const size = minSize + (maxSize - minSize) * scale;
		return `${size}rem`;
	}
</script>

<div class="relative p-8">
	{#each words as word, index}
		<div class="relative my-6">
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
					<div class="absolute right-full top-0 ml-4 w-64 rounded-lg bg-white p-4 shadow-lg">
						<div class="text-lg font-bold text-violet-800">{word.text}</div>
						<div class="mt-2 text-violet-600">{word.info}</div>
						<div class="mt-2 font-semibold text-violet-700">{word.percentage}%</div>
					</div>
				{/if}
			</div>
		</div>
	{/each}
</div>
