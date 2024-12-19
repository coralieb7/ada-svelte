<script>
  import Sortable from 'sortablejs';
  import { onMount } from 'svelte';

  // Define the correct order of items
  const correctOrder = [
      'LGBT',
      'Romance',
      'Comedy',
      'Drama',
      'World Cinema'
  ];

  // Create a reactive variable for the list items
  let items = [...correctOrder].sort(() => Math.random() - 0.5);

  let sortableInstance;
  let el;
  let verificationResult = '';

  onMount(() => {
      if (el) {
          sortableInstance = Sortable.create(el, {
              animation: 150,
              ghostClass: 'blue-background-class'
          });
      }
  });

  function verifyOrder() {
      // Get the current order of items
      const currentOrder = Array.from(el.children).map(li => li.textContent);

      // Compare the current order with the correct order
      const isCorrect = currentOrder.every((item, index) => item === correctOrder[index]);

      if (isCorrect) {
          verificationResult = 'Congrats! Perfect order!';
      } else {
          verificationResult = 'Not quite right. Here\'s the correct order:';
          // Reorder the items to the correct sequence
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
      {#each items as item (item)}
          <li 
              class="
                  p-3 
                  bg-white 
                  border 
                  rounded 
                  cursor-move 
                  hover:bg-blue-50 
                  transition 
                  shadow-sm
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

<style>
  .blue-background-class {
      opacity: 0.6;
      background-color: #e6f2ff;
  }
</style>