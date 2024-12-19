<script>
	import { scaleLinear } from 'd3';
	import { setContext } from 'svelte';
	import { writable } from 'svelte/store';
	import { tweened } from 'svelte/motion';

	import Timer from './Timer.svelte';
	import BarsF from './BarsFemale.svelte';
  import BarsM from './BarsMale.svelte';

	import AxisF from './AxisFemale.svelte';
  import AxisM from './AxisMale.svelte';

	import LabelsF from './LabelsFemale.svelte';
  import LabelsM from './LabelsMale.svelte';

	import Ticker from './Ticker.svelte';

	// Import both datasets
	import keyframesMale from '../../json/genres3_M.json';
	import keyframesFemale from '../../json/genres3_F.json';

	const duration = 300; // ms between keyframes
	const barCount = 6; // how many bars to show
	const barMargin = 4; // space between bars

	// Get names from both datasets
	const namesMale = keyframesMale[0][1].map((d) => d.name);
	const namesFemale = keyframesFemale[0][1].map((d) => d.name);

	// Create stores for both charts
	const dimensionsMale = writable({});
	const dimensionsFemale = writable({});
	const scalesMale = writable({});
	const scalesFemale = writable({});
	const dataMale = tweened(null, { duration });
	const dataFemale = tweened(null, { duration });
	const xMaxMale = tweened(null, { duration });
	const xMaxFemale = tweened(null, { duration });

	// Shared state for both charts
	let figureWidthMale = 0;
	let figureHeightMale = 0;
	let figureWidthFemale = 0;
	let figureHeightFemale = 0;
	let currentKeyframe = 0;
	let isPlaying = false;
	let sliderValue = 0;

	const maxFrames = Math.min(keyframesMale.length, keyframesFemale.length);

	// Function to handle slider change
	function handleSliderChange(event) {
		sliderValue = parseInt(event.target.value);
		currentKeyframe = sliderValue;
		isPlaying = false; // Pause when slider is manually changed
	}

	// Function to handle play/pause
	function togglePlay() {
		isPlaying = !isPlaying;
	}

	// Function to handle reset
	function handleReset() {
		currentKeyframe = 0;
		sliderValue = 0;
		isPlaying = false;
	}

	// Function to advance frames
	$: if (isPlaying && currentKeyframe < maxFrames - 1) {
		const timer = setTimeout(() => {
			currentKeyframe += 1;
			sliderValue = currentKeyframe;
			if (currentKeyframe >= maxFrames - 1) {
				isPlaying = false;
			}
			clearTimeout(timer);
		}, duration);
	}

	// update dimensions for male chart
	$: widthMale = figureWidthMale;
	$: heightMale = figureHeightMale;
	$: barHeightMale = heightMale / barCount - barMargin;

	// update dimensions for female chart
	$: widthFemale = figureWidthFemale;
	$: heightFemale = figureHeightFemale;
	$: barHeightFemale = heightFemale / barCount - barMargin;

	// Male chart data
	$: frameMale = keyframesMale[currentKeyframe];
	$: keyframeDateMale = frameMale[0];
	$: keyframeDataMale = frameMale[1];
	$: currentDataMale = namesMale.map((name) => ({
		...keyframeDataMale.find((d) => d.name == name)
	}));

	// Female chart data
	$: frameFemale = keyframesFemale[currentKeyframe];
	$: keyframeDateFemale = frameFemale[0];
	$: keyframeDataFemale = frameFemale[1];
	$: currentDataFemale = namesFemale.map((name) => ({
		...keyframeDataFemale.find((d) => d.name == name)
	}));

	// update stores for male chart
	$: dataMale.set(currentDataMale);
	$: dimensionsMale.set({
		width: widthMale,
		height: heightMale,
		barHeight: barHeightMale,
		barMargin
	});
	$: xMaxMale.set(Math.max(...keyframeDataMale.map((d) => d.value)));
	$: scalesMale.set({
		x: scaleLinear().domain([0, $xMaxMale]).range([0, widthMale]),
		y: scaleLinear().domain([0, barCount]).range([0, heightMale])
	});

	// update stores for female chart
	$: dataFemale.set(currentDataFemale);
	$: dimensionsFemale.set({
		width: widthFemale,
		height: heightFemale,
		barHeight: barHeightFemale,
		barMargin
	});
	$: xMaxFemale.set(Math.max(...keyframeDataFemale.map((d) => d.value)));
	$: scalesFemale.set({
		x: scaleLinear().domain([0, $xMaxFemale]).range([0, widthFemale]),
		y: scaleLinear().domain([0, barCount]).range([0, heightFemale])
	});

	// Set context for both charts
	$: {
		setContext('ChartMale', {
			dimensions: dimensionsMale,
			scales: scalesMale,
			data: dataMale,
			names: namesMale
		});
		setContext('ChartFemale', {
			dimensions: dimensionsFemale,
			scales: scalesFemale,
			data: dataFemale,
			names: namesFemale
		});
	}
</script>

{#if keyframesMale && keyframesFemale}
	<div class="charts-container">
		<!-- Male chart -->
		<div class="chart">
			<h2>Movies Directed by Men</h2>
			<figure bind:offsetWidth={figureWidthMale} bind:offsetHeight={figureHeightMale}>
				<div class="bars">
					<BarsM {barCount} context="ChartMale" />
				</div>

				<div class="axis">
					<AxisM context="ChartMale" />
				</div>

				<div class="labels">
					<LabelsM {barCount} context="ChartMale" />
				</div>
			</figure>
		</div>

		<!-- Female chart -->
		<div class="chart">
			<h2>Movies Directed by Women</h2>
			<figure bind:offsetWidth={figureWidthFemale} bind:offsetHeight={figureHeightFemale}>
				<div class="bars">
					<BarsF {barCount} context="ChartFemale" />
				</div>

				<div class="axis">
					<AxisF context="ChartFemale" />
				</div>

				<div class="labels">
					<LabelsF {barCount} context="ChartFemale" />
				</div>

				<div class="ticker">
					<Ticker date={keyframeDateFemale} />
				</div>
			</figure>
		</div>
	</div>
  <!-- Unified controls -->
	<div class="controls">
		<button
			on:click={togglePlay}
			class="rounded bg-emerald-400 px-4 py-2 text-white hover:bg-emerald-500"
		>
			{isPlaying ? 'Pause' : 'Play'}
		</button>
		<button
			on:click={handleReset}
			class="rounded bg-orange-400 px-4 py-2 text-white hover:bg-orange-500"
		>
			Reset
		</button>
		<input
			type="range"
			min="0"
			max={maxFrames - 1}
			bind:value={sliderValue}
			on:input={handleSliderChange}
			class="slider"
		/>
	</div>
{/if}

<style>
	.charts-container {
		display: grid;
		grid-template-columns: 1fr 1fr;
		gap: 2rem;
		margin-top: 1rem;
	}

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

	.controls {
		display: flex;
		align-items: center;
    justify-content: center;
		gap: 1rem;
		margin-bottom: 1rem;
	}

	.chart {
		margin-bottom: 2rem;
	}

	h2 {
		margin-bottom: 1rem;
		font-size: 1.25rem;
		font-weight: bold;
	}

	.slider {
		width: 100%;
		max-width: 300px;
		-webkit-appearance: none; /* Remove default styling in WebKit browsers */
		appearance: none; /* Remove default styling in modern browsers */
		height: 10px;
		background: #fef3c7;
		border-radius: 5px;
		outline: none;
		transition: background 0.3s;
	}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none; /* Remove default styling */
  appearance: none;
  width: 20px;
  height: 20px;
  background: #fbbf24;
  border-radius: 50%; /* Make it circular */
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  border: 2px solid #fff;
}

.slider::-moz-range-thumb {
  width: 20px;
  height: 20px;
  background: #fbbf24;
  border-radius: 50%; /* Make it circular */
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  border: 2px solid #fff;
}

.slider::-ms-thumb {
  width: 20px;
  height: 20px;
  background: #fbbf24;
  border-radius: 50%; /* Make it circular */
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  border: 2px solid #fff;
}
</style>
