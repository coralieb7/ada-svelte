<script>
	import { color } from 'd3';
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Load the data from the JSON file
		const response = await fetch('/json/female_char_in_time.json');
    	const data_json = await response.json();

		var trace1 = {
			x: Object.keys(data_json.male_directors),
			y: Object.values(data_json.male_directors),
			fill: 'tozeroy',
			type: 'scatter',
            name: 'Male Directors',
			fillcolor: 'rgba(23, 208, 125, 0.3)',
			line: { color: '#2D9884' }
		};

		var trace2 = {
			x: Object.keys(data_json.female_directors),
			y: Object.values(data_json.female_directors),
			fill: 'tozeroy',
			type: 'scatter',
            name: 'Female Directors',
			fillcolor: 'rgba(181, 107, 234, 0.3)',
			line: { color: '#c48bf0' }
		};

		var data = [trace1, trace2];
        var layout = {
            title: 'Representation of Female Characters over time by Director Gender',
            xaxis: { title: 'Years' },
            yaxis: { title: 'Percentage %' },
            template: 'plotly_white',
			width: 1000,
			height: 500
        };

		// Render the plot
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
