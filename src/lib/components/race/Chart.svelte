<script>
  import { scaleLinear } from "d3";
  import { setContext } from "svelte";
  import { writable } from "svelte/store";
  import { tweened } from "svelte/motion";
  
  import Timer from "./Timer.svelte";
  import Bars from "./Bars.svelte";
  import Axis from "./Axis.svelte";
  import Labels from "./Labels.svelte";
  import Ticker from "./Ticker.svelte";
  
  import keyframes_M from "../../json/genres3_M.json";
  import keyframes_F from "../../json/genres3_F.json";
  
  const duration = 300; // ms between keyframes
  const barCount = 8; // how many bars to show
  const barMargin = 4; // space between bars

  const keyframeCount_M = keyframes_M.length; // number of keyframes for genres3_M
  const keyframeCount_F = keyframes_F.length; // number of keyframes for genres3_F

  const names_M = keyframes_M[0][1].map((d) => d.name); // all data names/labels for genres3_M
  const names_F = keyframes_F[0][1].map((d) => d.name); // all data names/labels for genres3_F
  
  const dimensions = writable({});
  const scales = writable({});
  const data = tweened(null, { duration });
  const xMax = tweened(null, { duration });
  
  let figureWidth = 0;
  let figureHeight = 0;
  let currentKeyframe_M = 0;  // this is the index of the keyframes for genres3_M
  let currentKeyframe_F = 0;  // this is the index of the keyframes for genres3_F
  let isEnabled = false;
  
  // update dimensions
  $: width = figureWidth;
  $: height = figureHeight;
  $: barHeight = height / barCount - barMargin;
  
  // update data
  $: isEnabled = currentKeyframe_M < keyframeCount_M && currentKeyframe_F < keyframeCount_F;
  $: frameIndex_M = Math.min(currentKeyframe_M, keyframeCount_M - 1);
  $: frameIndex_F = Math.min(currentKeyframe_F, keyframeCount_F - 1);
  
  $: frame_M = keyframes_M[frameIndex_M];
  $: frame_F = keyframes_F[frameIndex_F];
  
  $: keyframeDate_M = frame_M[0];
  $: keyframeDate_F = frame_F[0];
  
  $: keyframeData_M = frame_M[1];
  $: keyframeData_F = frame_F[1];

  $: currentData_M = names_M.map((name) => ({
    ...keyframeData_M.find((d) => d.name == name),
  }));
  
  $: currentData_F = names_F.map((name) => ({
    ...keyframeData_F.find((d) => d.name == name),
  }));
  
  // update stores and context
  $: data.set({ M: currentData_M, F: currentData_F });
  $: dimensions.set({
    width,
    height,
    barHeight,
    barMargin,
  });
  $: xMax.set(Math.max(
    ...keyframeData_M.map((d) => d.value),
    ...keyframeData_F.map((d) => d.value)
  ));
  $: scales.set({
    x: scaleLinear().domain([0, $xMax]).range([0, $dimensions.width]),
    y: scaleLinear().domain([0, barCount]).range([0, $dimensions.height]),
  });
  $: chartContext = { dimensions, scales, data, names_M, names_F };
  $: setContext("Chart", chartContext);

  const yearRange = writable(0); // For the slider
  $: currentYear = $yearRange; // Bind year for chart updates
</script>

{#if keyframes_M && keyframes_F}
  <Timer
    bind:currentKeyframe_M
    bind:currentKeyframe_F
    keyframeCount_M="{keyframeCount_M}"
    keyframeCount_F="{keyframeCount_F}"
    duration="{duration}"
    isEnabled="{isEnabled}"
    on:end="{() => (isEnabled = false)}"
  />
  
  <figure bind:offsetWidth="{figureWidth}" bind:offsetHeight="{figureHeight}">
    <div class="bars">
      <Bars barCount="{barCount}" data="{currentData_M}" />
      <Bars barCount="{barCount}" data="{currentData_F}" />
    </div>
  
    <div class="axis">
      <Axis data="{currentData_M}" />
      <Axis data="{currentData_F}" />
    </div>
  
    <div class="labels">
      <Labels barCount="{barCount}" data="{currentData_M}" />
      <Labels barCount="{barCount}" data="{currentData_F}" />
    </div>
  
    <div class="ticker">
      <Ticker date="{keyframeDate_M}" />
      <Ticker date="{keyframeDate_F}" />
    </div>
  </figure>
  <!-- Container for slider -->
  <div class="slider-container">
    <input 
      type="range" 
      min="0" 
      max="{Math.max(keyframeCount_M, keyframeCount_F) - 1}" 
      bind:value="{currentYear}" 
      step="1"
      class="slider"
    />
    <div>Year: {currentYear}</div>
  </div>
{/if}

<style>
  figure {
    display: block;
    position: relative;
    width: 100%;
    height: 50vh;
    min-height: 420px;
    margin: 0;
    user-select: none;
  }

  figure > * {
    display: block;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
  }

  .axis {
    overflow: visible;
  }

  /* Container for the slider and timer */
  .slider-container {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 20px; /* space between timer and slider */
    position: relative;
    bottom: -10px; /* Adjusted for correct positioning */
  }

  /* Slider styles */
  .slider {
    width: 50%; /* Make the slider wider */
    height: 8px;
    background-color: #ddd;
    border-radius: 5px;
    -webkit-appearance: none;
    appearance: none;
  }

  .slider::-webkit-slider-thumb {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: #000000;
    -webkit-appearance: none;
  }

  .slider::-moz-range-thumb {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: #000000;
  }

</style>
