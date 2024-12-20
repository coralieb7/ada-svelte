<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Plot data
		const data = [
			{
				type: 'bar',
				y: [23.69230769230769, 76.3076923076923],
				x: ['Fail', 'Pass'], // Swap to have Fail in brighter part
				marker: { color: '#2D9884', size: 8 },
				name: 'Female Directors',
				domain: { row: 0, column: 0 },
				textinfo: 'none',
				hovertemplate:
					'%{x}<br>' + 'Proportion: %{y}<br>'
			},
			{
				type: 'bar',
				y: [47.1698113208, 52.83018867924528],
				x: ['Fail', 'Pass'], // Swap to have Fail in brighter part
				marker: { color: '#c48bf0', size: 8 },
				name: 'Male Directors',
				domain: { row: 0, column: 1 },
				textinfo: 'none',
				hovertemplate:
					'%{x}<br>' + 'Proportion: %{y}<br>'
			}
		];

		// Layout
		var layout = {
			barmode: 'group',
			title: {
				text: 'Bechdel Pass and Fail Distribution',
				font: {
					size: 24
				},
				x: 0.5
			},
			xaxis: { title: 'Rating' },
			yaxis: { title: 'Proportion (%) of movies' },
			template: 'plotly_white',
			width: 1050,
			height: 450
		};

		// Load Plotly and render the chart
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
