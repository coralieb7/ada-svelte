<script>
    import { getContext } from "svelte";
    import Bar from "./BarFemale.svelte";
    import colors from "./colorsF.json";
    const { data } = getContext("ChartFemale");
    const colorCount = colors.length;
    export let barCount;
  </script>
  
  {#each $data as { value, rank }, i (i)}
    {#if rank < barCount}
      <Bar value="{value}" rank="{rank}" fill="{colors[i % colorCount]}" />
    {/if}
  {/each}