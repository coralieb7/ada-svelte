<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Plot data
		const data = [
			{
				type: 'pie',
				values: [48.04281, 51.95719],
				labels: ['Fail', 'Pass'], 
				marker: {
					colors: ['#c48bf0', '#8059a4'] 
				},
				name: 'Female Directors',
				domain: { row: 0, column: 0 },
				textinfo: 'none',
				hovertemplate:
					'%{label}<br>' + 'Proportion: %{percent}<br>'
			},
			{
				type: 'pie',
				values: [ 41.768741, 58.231259],
				labels: [ 'Pass', 'Fail'],
				marker: {
					colors: ['#2D9884', '#17d07d'] 
				},
				name: 'Male Directors',
				domain: { row: 0, column: 1 },
				textinfo: 'none',
				hovertemplate:
					'%{label}<br>' + 'Proportion: %{percent}<br>'
			}
		];

		// Layout
		const layout = {
			title: 'Bechdel Test Fail and Pass',
			grid: { rows: 1, columns: 2 }, // Grid layout for two charts
			annotations: [
				
				{
					text: 'Female Directors',
					font: { size: 14 },
					showarrow: false,
					x: 0.23,
					y: -0.1, // Move below the pie chart
					xanchor: 'center',
					yanchor: 'top'
				},
				{
					text: 'Male Directors',
					font: { size: 14 },
					showarrow: false,
					x: 0.78,
					y: -0.1, // Move below the pie chart
					xanchor: 'center',
					yanchor: 'top'
				}
			],
			showlegend: false, // Remove the legend
			width: 1050,
			height: 450
		};

		// Load Plotly and render the chart
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
