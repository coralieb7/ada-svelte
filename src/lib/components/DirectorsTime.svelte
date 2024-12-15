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
			fillcolor: 'rgba(255, 165, 0, 0.3)',
			line: { color: 'orange' }
		};

		var trace2 = {
			x: Object.keys(data_json.female_directors),
			y: Object.values(data_json.female_directors),
			fill: 'tozeroy',
			type: 'scatter',
            name: 'Female Directors',
			fillcolor: 'rgba(65, 105, 225, 0.3)',
			line: { color: 'blue' }
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
