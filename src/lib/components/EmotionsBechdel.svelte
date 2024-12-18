<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Data for the first subplot (Bechdel passed)
		const response = await fetch('/json/emotion_bechdel.json');
		const data_json = await response.json();

		var trace1 = {
			type: 'scatterpolar',
			r: Object.values(data_json.male_directors), // Data for "Men - Bechdel passed"
			theta: Object.keys(data_json.male_directors),
			fill: 'toself',
			name: 'Men - Bechdel passed',
			line: { color: '#2D9884' }, // Yellow color
			fillcolor: 'rgba(45, 152, 132, 0.4)', // Semi-transparent yellow fill,
			subplot: 'polar1'
		};

		var trace2 = {
			type: 'scatterpolar',
			r: Object.values(data_json.female_directors), // Data for "Women - Bechdel passed"
			theta: Object.keys(data_json.female_directors),
			fill: 'toself',
			name: 'Women - Bechdel passed',
			line: { color: '#9467bd' }, // Blue color
			fillcolor: 'rgba(148, 103, 189, 0.4)', // Semi-transparent blue fill
            subplot: 'polar1'
		};

		// Data for the second subplot (Bechdel failed)
		var trace3 = {
			type: 'scatterpolar',
			r: Object.values(data_json.male_directors_no_bechdel), // Data for "Men - Bechdel failed"
			theta: Object.keys(data_json.male_directors_no_bechdel),
			fill: 'toself',
			name: 'Men - Bechdel failed',
			line: { color: '#17d07d' }, // Red color
			fillcolor: 'rgba(23, 208, 125, 0.4)', // Semi-transparent red fill
            subplot: 'polar2'
		};

		var trace4 = {
			type: 'scatterpolar',
			r: Object.values(data_json.female_directors_no_bechdel), // Data for "Women - Bechdel failed"
			theta: Object.keys(data_json.female_directors_no_bechdel),
			fill: 'toself',
			name: 'Women - Bechdel failed',
			line: { color: '#b56bea' }, // Dark blue color
			fillcolor: 'rgba(181, 107, 234, 0.4)', // Semi-transparent dark blue fill
            subplot: 'polar2'
		};

		// Create subplots (2 rows, 1 column)
		var data = [trace1, trace2, trace3, trace4];

		var layout = {
			title: 'Emotion Distribution by Gender for Bechdel Test Results',
			subplot_titles: ['Bechdel Passed', 'Bechdel Failed'],
			grid: { rows: 1, columns: 2, pattern: 'independent' },
			showlegend: true,
			template: 'plotly_white',
			polar: {
				angularaxis: {
					tickmode: 'array',
					tickvals: ['anger', 'sadness', 'fear', 'neutral', 'disgust', 'joy', 'surprise']
				}
			},
			polar1: {
				angularaxis: { tickmode: 'array', tickvals: ['anger', 'sadness', 'fear', 'neutral', 'disgust', 'joy', 'surprise'] },
                domain: { x: [0.1, 0.5], y: [0, 1] }
			},
			polar2: {
				angularaxis: { tickmode: 'array', tickvals: ['anger', 'sadness', 'fear', 'neutral', 'disgust', 'joy', 'surprise'] },
                domain: { x: [0.6, 1], y: [0, 1] }
			},
            legend: { x: 0.9, y: 1.05 },
			autosize: false,
			width: 900,
			height: 600,
        };

		// Render the plot with subplots
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
