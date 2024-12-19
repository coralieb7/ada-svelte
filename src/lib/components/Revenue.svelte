<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Load the data from the JSON file
		const response = await fetch('/json/revenue_bechdel.json');
		const data = await response.json();

		// Extract data arrays from the JSON
		const passedMale = Object.values(data.passed_male);
		const failedMale = Object.values(data.failed_male);
		const passedFemale = Object.values(data.passed_female);
		const failedFemale = Object.values(data.failed_female);

		// Define the Plotly figure
		const fig = {
			data: [
				{
					type: 'violin',
					y: passedMale,
					// name: 'Male Directors - Passed',
					line: { color: '#2D9884' },
					box: { visible: true }, // Show box plot within the violin
					meanline: { visible: true }, // Show mean line
					spanmode: 'soft'
				},
                {
					type: 'violin',
					y: passedFemale,
					// name: 'Female Directors - Passed',
					line: { color: '#9467bd' },
					box: { visible: true },
					meanline: { visible: true },
					spanmode: 'soft'
				},
				{
					type: 'violin',
					y: failedMale,
					// name: 'Male Directors - Failed',
					line: { color: '#17d07d' },
					box: { visible: true },
					meanline: { visible: true },
					spanmode: 'soft'
				},
				
				{
					type: 'violin',
					y: failedFemale,
					// name: 'Female Directors - Failed',
					line: { color: '#c48bf0' },
					box: { visible: true },
					meanline: { visible: true },
					spanmode: 'soft'
				}
			],
			layout: {
				title: {
					text: 'Revenue Distribution by Bechdel Test Results and Director Gender'
				},
				xaxis: {
                    title: 'Bechdel Passed                   Bechdel Failed',
					tickangle: -35 // Adjust for better label visibility
				},
				yaxis: {
					title: 'Revenue',
					tickprefix: '$', // Add dollar sign for y-axis labels
					zeroline: true
				},
				legend: {
					title: { text: 'Categories' }
				},
				margin: { l: 100, r: 50, t: 50, b: 150 },
				colorway: ['#c48bf0', '#17d07d', '#9467bd', '#2D9884'], // Set consistent colors,
				autosize: false,
				width: 1050,
				height: 500
			}
		};

		// Render the plot
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, fig.data, fig.layout);
	});
</script>

<div bind:this={plotElement}></div>
