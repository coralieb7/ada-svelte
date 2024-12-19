<script>
	import { onMount } from 'svelte';

	let plotElement;

	onMount(async () => {
		// Load the data from the JSON file
		const response = await fetch('/json/success_bechdel.json');
		const data = await response.json();

		// Map the data fields
		const averageRatings = data.map((d) => d.average_rating);
		const boxOfficeRevenue = data.map((d) => d.box_office_revenue);
		const movieBudget = data.map((d) => d.movie_budget);
		const directorGender = data.map((d) => d.director_gender);
		const movieNames = data.map((d) => d.movie_name);

		// Define colors and labels for gender mapping
		const colorMap = {
			M: '#2D9884',
			F: '#9467bd'
		};
		const genderLabels = {
			M: 'Male Director',
			F: 'Female Director'
		};

		// Separate data by gender for legend distinction
		const maleDirectorData = data.filter((d) => d.director_gender === 'M');
		const femaleDirectorData = data.filter((d) => d.director_gender === 'F');

		const fig = {
			data: [
				// Male Director Data
				{
					x: maleDirectorData.map((d) => d.average_rating),
					y: maleDirectorData.map((d) => d.box_office_revenue),
					text: maleDirectorData.map((d) => d.movie_name),
					mode: 'markers',
					marker: {
						size: maleDirectorData.map((d) => Math.sqrt(d.movie_budget) / 500), // Scaled size for visualization
						color: colorMap.M,
						opacity: 0.7
					},
					name: genderLabels.M, // Adds to the legend
					hovertemplate: '<b>%{text}</b><br>Rating: %{x}<br>Revenue: %{y}<br>Budget: $%{customdata}<extra></extra>',
					customdata: maleDirectorData.map((d) => d.movie_budget) // Attach the original budget for hover display
				},
				// Female Director Data
				{
					x: femaleDirectorData.map((d) => d.average_rating),
					y: femaleDirectorData.map((d) => d.box_office_revenue),
					text: femaleDirectorData.map((d) => d.movie_name),
					mode: 'markers',
					marker: {
						size: femaleDirectorData.map((d) => Math.sqrt(d.movie_budget) / 1000), // Scaled size for visualization
						color: colorMap.F,
						opacity: 0.7
					},
					name: genderLabels.F, // Adds to the legend
					hovertemplate: '<b>%{text}</b><br>Rating: %{x}<br>Revenue: %{y}<br>Budget: $%{customdata}<extra></extra>',
					customdata: femaleDirectorData.map((d) => d.movie_budget) // Attach the original budget for hover display
				}
			],
			layout: {
				title: 'Proportional Average Rating of Movies by Director Gender',
				xaxis: { title: 'Average Rating' },
				yaxis: { title: 'Box Office Revenue' },
				width: 1050,
				height: 500,
				legend: { title: { text: 'Director Gender' } }
			}
		};

		// Render the plot
		const Plotly = await import('plotly.js-dist');
		Plotly.newPlot(plotElement, fig.data, fig.layout);
	});
</script>

<div bind:this={plotElement}></div>
