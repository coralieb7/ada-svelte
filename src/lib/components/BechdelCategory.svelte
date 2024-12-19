<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Plot data
		const data = [
			{
				type: 'pie',
				values: [23.69230769230769, 76.3076923076923],
				labels: ['Fail', 'Pass'], // Swap to have Fail in brighter part
				marker: {
					colors: ['#c48bf0', '#8059a4'] // Assign the brightest color to Fail
				},
				name: 'Female Directors',
				domain: { row: 0, column: 1 },
				textinfo: 'none',
				hovertemplate:
					'%{label}<br>' + 'Proportion: %{percent}<br>'
			},
			{
				type: 'pie',
				values: [47.1698113208, 52.83018867924528],
				labels: ['Fail', 'Pass'], // Swap to have Fail in brighter part
				marker: {
					colors: ['#17d07d', '#2D9884'] // Assign the brightest color to Fail
				},
				name: 'Male Directors',
				domain: { row: 0, column: 0 },
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
					text: 'Male Directors',
					font: { size: 14 },
					showarrow: false,
					x: 0.23,
					y: -0.1, // Move below the pie chart
					xanchor: 'center',
					yanchor: 'top'
				},
				{
					text: 'Female Directors',
					font: { size: 14 },
					showarrow: false,
					x: 0.78,
					y: -0.1, // Move below the pie chart
					xanchor: 'center',
					yanchor: 'top'
				}
			],
			showlegend: false, // Remove the legend
			height: 500,
			width: 800
		};

		// Load Plotly and render the chart
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
