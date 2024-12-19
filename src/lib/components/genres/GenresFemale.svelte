<script>
import { onMount } from 'svelte';
import Sortable from 'sortablejs';

const correctOrder = [
    'LGBT',
    'Romance',
    'Comedy',
    'Drama',
    'World Cinema'
];

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
    const currentOrder = Array.from(el.children).map(li => li.textContent);
    const isCorrect = currentOrder.every((item, index) => item === correctOrder[index]);
    
    isVerified = true;
    
    // Disable dragging after verification
    if (sortableInstance) {
        sortableInstance.option("disabled", true);
    }
    
    if (isCorrect) {
        verificationResult = 'Congrats! Perfect order!';
    } else {
        verificationResult = 'Not quite right. Here\'s the correct order!';
        items = [...correctOrder];
    }
}
</script>

<div class="max-w-md mx-auto p-6 bg-gray-50 border-2 border-orange-500 rounded-lg shadow-md">
    <h2 class="text-xl font-bold mb-4">Top-5 Genres - Female directors</h2>
    
    <ul 
        bind:this={el} 
        class="space-y-2 mb-4"
    >
        {#each items as item, index (item)}
            <li 
                class="
                    p-3 
                    border 
                    rounded 
                    {!isVerified ? 'cursor-move hover:bg-blue-50' : ''} 
                    transition 
                    shadow-sm
                    {isVerified ? 
                        (item === correctOrder[index] ? 
                            'bg-green-100 border-green-400' : 
                            'bg-red-100 border-red-400'
                        ) : 
                        'bg-white'
                    }
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
            bg-yellow-300 
            text-white 
            py-2 
            rounded 
            hover:bg-yellow-400 
            transition
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