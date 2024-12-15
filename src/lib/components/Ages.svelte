<script>
  import { onMount } from 'svelte';

  let plotElement;

  onMount(async () => {
    // Load the data from the JSON file
    const response = await fetch('/json/ages.json');
    const data = await response.json();

    const fig = {
      data: [
        {
          type: 'scatter',
          mode: 'lines',
          x: Object.keys(data.female_female_percentage),
          y: Object.values(data.female_female_percentage),
          name: 'Female Actors (Female Directors)',
          line: { color: 'blue' },
        },
        {
          type: 'scatter',
          mode: 'lines',
          x: Object.keys(data.female_male_percentage),
          y: Object.values(data.female_male_percentage),
          name: 'Male Actors (Female Directors)',
          line: { color: 'orange' },
        },
        {
          type: 'scatter',
          mode: 'lines',
          x: Object.keys(data.male_female_percentage),
          y: Object.values(data.male_female_percentage),
          name: 'Female Actors (Male Directors)',
          line: { color: 'lightblue', dash: 'dash' },
        },
        {
          type: 'scatter',
          mode: 'lines',
          x: Object.keys(data.male_male_percentage),
          y: Object.values(data.male_male_percentage),
          name: 'Male Actors (Male Directors)',
          line: { color: 'orange', dash: 'dash' },
        },
      ],
      layout: {
        title: 'Age Distribution of Actors by Director Gender (Percentage)',
        xaxis: { title: 'Age' },
        yaxis: { title: 'Percentage (%)' },
        legend: { title: 'Actor Gender & Director Gender' },

        template: 'plotly_dark',
      },
    };

    // Render the plot
    const Plotly = await import('plotly.js-dist');
    Plotly.newPlot(plotElement, fig.data, fig.layout);
  });
</script>

<div bind:this={plotElement}></div>
