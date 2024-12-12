<script>
  import { onMount } from "svelte";
  let plotDiv;
  let Plotly;

  export let data = [];
  export let layout = {};

  // Ensure Plotly is loaded only in the browser
  onMount(async () => {
    Plotly = await import("plotly.js-dist"); // Use the "dist" version for browser compatibility
    Plotly.newPlot(plotDiv, data, layout);

  });
</script>

<div bind:this={plotDiv} class="w-full h-full"></div>
