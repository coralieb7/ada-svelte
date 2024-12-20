<script>
	let flipped = Array(9).fill(false);

	const cards = [
		{
			image: '/img/square.png',
			frontText: 'Midnight Express',
			backText: 'Fails',
			grade: '0/3',
			passes: false
		},
		{
			image: '/img/square.png',
			frontText: 'Ratatouille',
			backText: 'Fails',
			grade: '1/3',
			passes: false
		},
		{
			image: '/img/square.png',
			frontText: 'Harry Potter 4',
			backText: 'Fails',
			grade: '1/3',
			passes: false
		},
		{
			image: '/img/square.png',
			frontText: 'Pulp Fiction',
			backText: 'Passes',
			grade: '3/3',
			passes: true
		},
		{
			image: '/img/square.png',
			frontText: 'Barbie: Fairytopia',
			backText: 'Passes',
			grade: '3/3',
			passes: true
		},
		{
			image: '/img/square.png',
			frontText: 'The Grand Budapest Hotel',
			backText: 'Fails',
			grade: '1/3',
			passes: false
		},
		{
			image: '/img/square.png',
			frontText: 'Oppenheimer',
			backText: 'Fails',
			grade: '2/3',
			passes: false
		},
		{
			image: '/img/square.png',
			frontText: 'Titanic',
			backText: 'Passes',
			grade: '3/3',
			passes: true
		},

		{
			image: '/img/square.png',
			frontText: 'The Avengers',
			backText: 'Fails',
			grade: '1/3',
			passes: false
		}
	];

	function handleFlip(index) {
		flipped[index] = !flipped[index];
		flipped = [...flipped]; // trigger reactivity
	}
</script>

<div class="flex flex-col items-center gap-6 p-4">
	<h3 class="text-2xl font-bold">Movie Memory Game</h3>
	<p class="text-gray-600">Click on the cards to reveal their Bechdel Test results!</p>
	<div class="grid grid-cols-3 gap-4">
		{#each cards as card, index}
			<button
				on:click={() => handleFlip(index)}
				on:keydown={(e) => e.key === 'Enter' && handleFlip(index)}
				class="perspective-1000 relative h-40 w-40 cursor-pointer"
				aria-label={`Card ${index + 1}`}
			>
				<div
					class="transform-style-3d absolute inset-0 h-full w-full transition-transform duration-500"
					class:rotate-y-180={flipped[index]}
				>
					<!-- Front of card -->
					<div
						class="backface-hidden absolute inset-0 h-full w-full items-center justify-center rounded-lg border-2 border-yellow-300 bg-white p-9 shadow-lg"
					>
						<p class="text-md font-semibold">{card.frontText}</p>
					</div>

					<!-- Back of card -->
					<div
						class="rotate-y-180 backface-hidden absolute inset-0 flex h-full w-full transform flex-col gap-4 rounded-lg border-2 bg-white p-4 shadow-lg"
						class:border-emerald-300={card.passes}
						class:border-red-300={!card.passes}
					>
						<p class="text-sm">{card.frontText}</p>
						<p class="text-md font-bold">{card.backText}</p>
						<p class="text-md">{card.grade}</p>
					</div>
				</div>
			</button>
		{/each}
	</div>
</div>

<style>
	.perspective-1000 {
		perspective: 1000px;
	}
	.transform-style-3d {
		transform-style: preserve-3d;
	}
	.backface-hidden {
		backface-visibility: hidden;
	}
	.rotate-y-180 {
		transform: rotateY(180deg);
	}
</style>
