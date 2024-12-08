<script>
  import { onMount } from "svelte";
  let plotDiv;
  let Plotly;

  export let data = [];
  export let layout = {};
  export let config = {};

  // Ensure Plotly is loaded only in the browser
  onMount(async () => {
    Plotly = await import("plotly.js-dist"); // Use the "dist" version for browser compatibility
    Plotly.newPlot(plotDiv, data, layout, config);

    return () => {
      if (Plotly && plotDiv) {
        Plotly.purge(plotDiv); // Cleanup on component unmount
      }
    };
  });

  $: {
    if (Plotly && plotDiv) {
      Plotly.react(plotDiv, data, layout, config); // Update plot dynamically
    }
  }
</script>

<div bind:this={plotDiv} class="w-full h-full"></div>
