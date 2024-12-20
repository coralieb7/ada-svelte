<script>
	import { onMount } from 'svelte';
	import Sortable from 'sortablejs';

	const correctOrder = ['LGBT', 'Romance', 'Comedy'];

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

	function verifyOrder() {
		const currentOrder = Array.from(el.children).map((li) => li.textContent);
		const isCorrect = currentOrder.every((item, index) => item === correctOrder[index]);

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

<div class="mx-auto max-w-md text-center rounded-lg border-2 border-violet-400 bg-gray-50 p-6 shadow-md">
	<h2 class="mb-4 text-xl font-bold">Top-3 Genres with the most Female Characters - Female directors</h2>

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
					? item === correctOrder[index]
						? 'border-orange-400 bg-orange-100'
						: 'border-yellow-400 bg-yellow-100'
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
            bg-violet-300
            py-2
            text-white
            transition
            hover:bg-violet-400
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
                {verificationResult.includes('Congrats') ? 'text-yellow-600' : 'text-orange-600'}
            "
		>
			{verificationResult}
		</p>
	{/if}
</div>
