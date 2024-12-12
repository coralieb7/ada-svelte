<script>
    import { getContext } from "svelte";
    import Tick from "/Users/coraliebanuls/Library/CloudStorage/OneDrive-Personal/Documents/EPFL/MA1/ADA/ada-svelte/src/lib/components/race/Tick.svelte";
    const { scales } = getContext("Chart");
    $: ticks = $scales.x.ticks(5).slice(1); // don't need to show 0
  </script>
  
  {#each ticks as value (value)}
    <Tick x="{$scales.x(value)}" value="{value}" />
  {/each}