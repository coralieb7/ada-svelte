<script>
	import { color } from 'd3';
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Load the data from the JSON file
		const response = await fetch('/json/ages.json');
		const data = await response.json();

		const fig = {
			data: [
				{
					type: 'scatter',
					mode: 'lines',
					x: Object.keys(data.female_female_percentage),
					y: Object.values(data.female_female_percentage),
					name: 'Female Actors (Female Directors)',
					line: { color: 'blue' }
				},
				{
					type: 'scatter',
					mode: 'lines',
					x: Object.keys(data.female_male_percentage),
					y: Object.values(data.female_male_percentage),
					name: 'Male Actors (Female Directors)',
					line: { color: 'orange' }
				},
				{
					type: 'scatter',
					mode: 'lines',
					x: Object.keys(data.male_female_percentage),
					y: Object.values(data.male_female_percentage),
					name: 'Female Actors (Male Directors)',
					line: { color: 'lightblue', dash: 'dash' }
				},
				{
					type: 'scatter',
					mode: 'lines',
					x: Object.keys(data.male_male_percentage),
					y: Object.values(data.male_male_percentage),
					name: 'Male Actors (Male Directors)',
					line: { color: 'orange', dash: 'dash' }
				}
			],
			layout: {
        title: {
          text: "Actor's Age Distribution",
          font: {
            size: 24,
            color: 'white'
        }},
				xaxis: { title: 'Age', color: 'white' },
				yaxis: { title: 'Percentage (%)', color: 'white' },
				legend: { title:{text:'Actor Gender & Director Gender', font:{color:'white'}}, font: {color: 'white'}  },
        paper_bgcolor: '#4c1d95',
        plot_bgcolor: '#4c1d95',
        color: 'white'
			}
		};
		// Render the plot
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, fig.data, fig.layout);
	});
</script>

<div bind:this={plotElement}></div>
