<script>
	import { color } from 'd3';
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Load the data from the JSON file
		const response = await fetch('/json/emotion_data_distribution_emotions.json');
		const data_json = await response.json();

		var trace1 = {
			type: 'scatterpolar',
			r: Object.values(data_json.female_directors),
			theta: Object.keys(data_json.female_directors),
			fill: 'toself',
			name: 'Female Directors'
		};

		var trace2 = {
			type: 'scatterpolar',
			r: Object.values(data_json.male_directors),
			theta: Object.keys(data_json.male_directors),
			fill: 'toself',
			name: 'Male Directors'
		};

		var data = [trace1, trace2];
		var layout = {
			title: 'Ratio of Emotions in Plot Summaries by Director Gender',
			template: 'plotly_white',
			polar: {
				angularaxis: {
					tickmode: 'array',
					tickvals: ['anger', 'sadness', 'fear', 'neutral', 'disgust', 'joy', 'surprise']
				}
			}
		};
		// Render the plot
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
