<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Plot data
		const data = [
			{
				type: 'pie',
				values: [18.864097, 81.135903],
				labels: ['Female tropes', 'Male tropes'],
				text: [
					'FinalGirl, <br> DumbBlonde, <br> BrokenBird, <br> BrainlessBeauty,<br> ValleyGirl, <br>ClassyCatBurglar',
					'DirtyCop, CorruptCorporateExecutive, <br>PsychoForHire, TranquilFury, <br>JerkJock, CrazyJealousGuy, <br>HenpeckedHusband, GrumpyOldMan,<br>StupidCrooks, ByronicHero, <br>CulturedBadass, DeanBitterman, <br>DumbMuscle, SelfMadeMan, <br>HitmanWithAHeart, Revenge'
				],
				marker: {
					colors: ['#c48bf0', '#2D9884']
				},
				name: 'Male Directors',
				hole: 0.6,
				domain: { row: 0, column: 0 },
				textinfo: 'none',
				hovertemplate:
					'%{label}<br>' + 'Proportion: %{percent}<br>' + 'Tropes: <br> %{text}<extra></extra>'
			},
			{
				type: 'pie',
				values: [51.612903, 48.387097],
				labels: ['Female tropes', 'Male tropes'],
				text: [
					'FinalGirl, <br> DumbBlonde, <br> ValleyGirl, <br> BrainlessBeauty,<br> BrokenBird, <br>ClassyCatBurglar',
					'SurferDude, ChildProdigy, <br>ByronicHero, MorallyBankruptBanker, <br>EccentricMentor, HenpeckedHusband, <br>GadgeteerGenius, JerkJock,<br>FatherToHisMen, DumbMuscle, <br>RomanticRunnerup, CrazyJealousGuy, <br>TranquilFury, CorruptCorporateExecutive, <br>MasterSwordsman, DirtyCop,<br> CulturedBadass’'
				],

				marker: {
					colors: ['#c48bf0', '#2D9884']
				},
				name: 'Female Directors',
				hole: 0.6,
				domain: { row: 0, column: 1 },
				textinfo: 'none',
				hovertemplate:
					'%{label}<br>' + 'Proportion: %{percent}<br>' + 'Tropes: <br> %{text}<extra></extra>'
			}
		];

		// Layout
		const layout = {
			title: 'Representation of Gendered Tropes by Director Gender',
			grid: { rows: 1, columns: 2 }, // Grid layout for two charts
			annotations: [
				{
					text: 'Male Directors',
					font: { size: 14 },
					showarrow: false,
					x: 0.15,
					y: 0.5
				},
				{
					text: 'Female Directors',
					font: { size: 14 },
					showarrow: false,
					x: 0.87,
					y: 0.5
				}
			],
			showlegend: true, // Show legend below
			height: 500,
			width: 800
		};

		// Load Plotly and render the chart
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, data, layout);
	});
</script>

<div bind:this={plotElement}></div>
