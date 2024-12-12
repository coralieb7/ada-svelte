<script>
  import ChartM from './Chart.svelte';
  import ChartF from './Chart_F.svelte';
  import Timer from "./Timer.svelte";

  import { onMount } from 'svelte';

</script>

<div class="container">
  <div class="flex min-h-screen">
    <div class="w-1/2">
      <ChartM />
    </div>
    <div class="w-1/2">
      <ChartF />
    </div>
  </div>
</div>
