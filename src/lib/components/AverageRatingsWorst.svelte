<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Load the data from the JSON file
		const response = await fetch('/json/ratings.json');
		const data_json = await response.json();

		var traces1 = {
			x: Object.values(data_json.worst_female_ratings.average_ratings),
			y: Object.values(data_json.worst_female_ratings.percentage),

			name: 'Female Directors',
			type: 'bar',
			marker: { color: '#c48bf0', size: 8 }
		};
		var traces2 = {
			x: Object.values(data_json.worst_male_ratings.average_ratings),
			y: Object.values(data_json.worst_male_ratings.percentage),
			name: 'Male Directors',
			type: 'bar',
			marker: { color: '#2D9884', size: 8 }
		};
		var data = [traces1, traces2];
		var layout = {
			barmode: 'group',
			title: 'Worst group',
			xaxis: { title: 'Rating' },
			yaxis: { title: 'Percentage %' },
			autosize: false,
			width: 600,
			height: 400
		};
		var config = { responsive: true };

		// Render the plot
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout, config);
	});
</script>

<div bind:this={plotElement}></div>
