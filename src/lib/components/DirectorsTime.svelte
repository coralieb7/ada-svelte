<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Load the data from the JSON file
		

		var trace1 = {
			x: [1, 2, 3, 4],
			y: [0, 2, 3, 5],
			fill: 'tozeroy',
			type: 'scatter',
            name: 'Male Directors'
		};

		var trace2 = {
			x: [1, 2, 3, 4],
			y: [3, 5, 1, 7],
			fill: 'tonexty',
			type: 'scatter',
            name: 'Female Directors'
		};

		var data = [trace1, trace2];
        var layout = {
            title: 'Representation of Female Characters over time by Director Gender',
            xaxis: { title: 'Years' },
            yaxis: { title: 'Percentage %' },
            template: 'plotly_white'
        };

		// Render the plot
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
