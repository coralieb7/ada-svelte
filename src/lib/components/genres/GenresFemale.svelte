<script>
	import { onMount } from 'svelte';
	import Sortable from 'sortablejs';

	const correctOrder = ['LGBT', 'Romance', 'Comedy', 'Drama', 'World Cinema'];

	let items = [...correctOrder].sort(() => Math.random() - 0.5);
	let sortableInstance;
	let el;
	let verificationResult = '';
	let isVerified = false;

	onMount(() => {
		if (el) {
			sortableInstance = Sortable.create(el, {
				animation: 150,
				ghostClass: 'blue-background-class',
				disabled: false
			});
		}
	});

	function isItemInCorrectPosition(item, index) {
		return item === correctOrder[index];
	}

	function verifyOrder() {
		const currentOrder = Array.from(el.children).map((li) => li.textContent);
		const isCorrect = currentOrder.every((item, index) => isItemInCorrectPosition(item, index));

		isVerified = true;

		// Disable dragging after verification
		if (sortableInstance) {
			sortableInstance.option('disabled', true);
		}

		if (isCorrect) {
			verificationResult = 'Congrats! Perfect order!';
		} else {
			verificationResult = "Not quite right. Here's the correct order!";
			items = [...correctOrder];
		}
	}
</script>

<div class="mx-auto max-w-md rounded-lg border-2 border-orange-500 bg-gray-50 p-6 shadow-md">
	<h2 class="mb-4 text-xl font-bold">Top-5 Genres - Female directors</h2>

	<ul bind:this={el} class="mb-4 space-y-2">
		{#each items as item, index (item)}
			<li
				class="
                    rounded
                    border
                    p-3
                    {!isVerified ? 'cursor-move hover:bg-blue-50' : ''} 
                    shadow-sm
                    transition
                    {isVerified
					? isItemInCorrectPosition(item, index)
						? 'border-green-400 bg-green-100'
						: 'border-red-400 bg-red-100'
					: 'bg-white'}
                "
			>
				{item}
			</li>
		{/each}
	</ul>

	<button
		on:click={verifyOrder}
		class="
            w-full
            rounded
            bg-yellow-300
            py-2
            text-white
            transition
            hover:bg-yellow-400
        "
		disabled={isVerified}
	>
		Verify Order
	</button>

	{#if verificationResult}
		<p
			class="
                mt-4
                text-center
                {verificationResult.includes('Congrats') ? 'text-green-600' : 'text-violet-600'}
            "
		>
			{verificationResult}
		</p>
	{/if}
</div>
