<script>
    import { getContext } from "svelte";
    import Bar from "./BarMale.svelte";
    import colors from "./colorsM.json";
    const { data } = getContext("ChartMale");
    const colorCount = colors.length;
    export let barCount;
  </script>
  
  {#each $data as { value, rank }, i (i)}
    {#if rank < barCount}
      <Bar value="{value}" rank="{rank}" fill="{colors[i % colorCount]}" />
    {/if}
  {/each}