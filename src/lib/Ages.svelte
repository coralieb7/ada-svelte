<script>
  import { onMount } from 'svelte';

  let plotElement;

  onMount(async () => {
    // Dynamically import Plotly.js-dist
    const Plotly = await import('plotly.js-dist');

    // Sample data (replace with your actual data)
    const female_directed_female = [20, 30, 50]; // Replace with actual filtered data
    const female_directed_male = [30, 40, 60]; // Replace with actual filtered data
    const male_directed_female = [40, 50, 60]; // Replace with actual filtered data
    const male_directed_male = [10, 15, 20]; // Replace with actual filtered data

    // Create normalized percentage data (use your actual data transformation here)
    const female_female_percentage = [20, 30, 50]; // Example
    const female_male_percentage = [30, 40, 60]; // Example
    const male_female_percentage = [40, 50, 60]; // Example
    const male_male_percentage = [10, 15, 20]; // Example

    // Create the Plotly figure
    const fig = {
      data: [
        // Female directors
        {
          type: 'scatter',
          mode: 'lines',
          x: [20, 30, 40], // Replace with actual age data
          y: female_female_percentage,
          name: 'Female Actors (Female Directors)',
          line: { color: 'blue' },
        },
        {
          type: 'scatter',
          mode: 'lines',
          x: [20, 30, 40], // Replace with actual age data
          y: female_male_percentage,
          name: 'Male Actors (Female Directors)',
          line: { color: 'orange' },
        },
        // Male directors
        {
          type: 'scatter',
          mode: 'lines',
          x: [20, 30, 40], // Replace with actual age data
          y: male_female_percentage,
          name: 'Female Actors (Male Directors)',
          line: { color: 'lightblue', dash: 'dash' },
        },
        {
          type: 'scatter',
          mode: 'lines',
          x: [20, 30, 40], // Replace with actual age data
          y: male_male_percentage,
          name: 'Male Actors (Male Directors)',
          line: { color: 'orange', dash: 'dash' },
        },
      ],
      layout: {
        title: 'Age Distribution of Actors by Director Gender (Percentage)',
        xaxis: { title: 'Age' },
        yaxis: { title: 'Percentage (%)' },
        legend: { title: 'Actor Gender & Director Gender' },
        template: 'plotly_white',
      },
    };

    // Render the plot once Plotly is available
    Plotly.newPlot(plotElement, fig.data, fig.layout);
  });
</script>

<!-- HTML to bind Plotly plot -->
<div bind:this={plotElement} style="height: 500px;"></div>
