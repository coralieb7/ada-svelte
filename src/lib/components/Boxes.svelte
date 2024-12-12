<script>
	let boxes = [
		{ id: 1, text: 'Feminist', color: '#FFDE6B' },
		{ id: 2, text: 'Religious', color: '#EF89EE' },
		{ id: 3, text: 'Health and Fitness', color: '#F79F1E' },
		{ id: 4, text: 'Drama', color: '#02B8FF' },
		{ id: 5, text: 'Pornography', color: '#9F84EC' }
	];

	let slots = [null, null, null, null, null]; // Initially, all slots are empty

	const correctOrder = [1, 4, 3, 5, 2]; // IDs in the correct order for validation
	let feedback = '';

	function handleDragStart(event, box) {
		event.dataTransfer.setData('text/plain', JSON.stringify(box));
	}

	function handleDragOver(event) {
		event.preventDefault(); // Allows drop
	}

	function handleDrop(event, index) {
		const box = JSON.parse(event.dataTransfer.getData('text/plain'));
		if (!slots[index]) {
			slots[index] = box; // Place the box in the slot
			boxes = boxes.filter((b) => b.id !== box.id); // Remove it from the draggable boxes
		}
	}

	function resetGame() {
		// Reset slots and boxes to initial state
		slots = [null, null, null, null, null];
		boxes = [
			{ id: 1, text: 'Feminist', color: '#FFDE6B' },
			{ id: 2, text: 'Religious', color: '#EF89EE' },
			{ id: 3, text: 'Health and Fitness', color: '#F79F1E' },
			{ id: 4, text: 'Drama', color: '#02B8FF' },
			{ id: 5, text: 'Pornography', color: '#9F84EC' }
		];
		feedback = ''; // Clear feedback
	}

	function verifyPlacement() {
		// Check if the boxes are in the correct order
		let isCorrect = true;
		let id = 0;
		let ids = [];
		let indexes = [];

		// Verify the slots against the correct order
		slots.forEach((slot, index) => {
			// Check if the slot is empty (no box assigned)
			if (!slot || !slot.id || slot.id !== correctOrder[index]) {
				isCorrect = false;
				id = slot.id;
				ids.push(id);
				indexes.push(index);
			}
		});

		if (isCorrect) {
			feedback = 'Well done! All genres are correctly placed!';
		} else {
			feedback = 'Incorrect! The correct placements will now be displayed.';
			setTimeout(() => {
				// Update only the incorrect slots using the ids and indexes
				slots = slots.map((slot, index) => {
					if (indexes.includes(index)) {
						// If the slot is empty (no box), assign the correct box to it
						const correctBox = boxes.find((box) => box.id === correctOrder[index]);

						if (correctBox) {
							return {
								...slot,
								color: 'gray', // Change the color to gray if the box was wrong or empty
								text: correctBox.text || `Genre ${correctOrder[index]}` // Display the correct genre text
							};
						}
					}
					return slot; // Return the slot as is if it was already correct
				});

				// Empty the draggable section
				boxes = [];
			}, 1000); // Correct the slots after 1 second
		}
	}
</script>

<!-- Slots Section -->
<div class="slots">
	{#each slots as slot, index}
		<div
			class="slot"
			role="listbox"
			aria-dropeffect="move"
			tabindex="0"
			on:drop={(event) => handleDrop(event, index)}
			on:dragover={handleDragOver}
		>
			{#if slot}
				<div
					class="box"
					style="background-color: {slot.color};"
					role="option"
					aria-grabbed="false"
					aria-selected="true"
					tabindex="0"
					draggable="true"
				>
					{slot.text}
				</div>
			{/if}
		</div>
	{/each}
</div>

<!-- Draggable Boxes Section -->
<div class="boxes">
	{#each boxes as box}
		<div
			class="box"
			style="background-color: {box.color};"
			role="option"
			aria-grabbed="false"
			aria-selected="false"
			tabindex="0"
			draggable="true"
			on:dragstart={(event) => handleDragStart(event, box)}
		>
			{box.text}
		</div>
	{/each}
</div>

<!-- Feedback Section -->
<p class="feedback">{feedback}</p>

<!-- Verify and Reset Buttons -->
<div class="controls">
	<button on:click={verifyPlacement} class="verify-button"> Verify </button>
	<button on:click={resetGame} class="again-button"> Again </button>
</div>

<style>
	.slots {
		display: flex;
		justify-content: center;
		gap: 10px;
		margin-bottom: 20px;
	}
	.slot {
		width: 100px;
		height: 100px;
		border: 2px dashed #ccc;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.boxes {
		display: flex;
		justify-content: center;
		gap: 10px;
	}
	.box {
		width: 100px;
		height: 100px;
		display: flex;
		align-items: center;
		justify-content: center;
		color: white;
		font-weight: bold;
		cursor: grab;
		user-select: none;
	}
	.controls {
		display: flex;
		justify-content: center;
		margin-top: 20px;
		gap: 10px;
	}
	.again-button {
		padding: 10px 20px;
		font-size: 16px;
		background-color: #f04e98;
		color: white;
		border: none;
		border-radius: 5px;
		cursor: pointer;
	}
	.again-button:hover {
		background-color: #cd3d7e;
	}
	.verify-button {
		padding: 10px 20px;
		font-size: 16px;
		background-color: #a2cb39;
		color: white;
		border: none;
		border-radius: 5px;
		cursor: pointer;
	}
	.verify-button:hover {
		background-color: #85a730;
	}
</style>
