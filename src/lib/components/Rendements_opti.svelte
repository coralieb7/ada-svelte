<script>
    import { onMount } from 'svelte';
  
    let plotElement;
  
    onMount(async () => {
        const response = await fetch('/json/opti_vs_worst_rendement.json');
        const data_json = await response.json();
  
      const data = [
        {
          type: 'box',
          y: Object.values(data_json.opti_male_rendement),
          name: 'Male Directors',  // Male
          marker: {
            color: '#17d07d'
          },
          boxmean: 'sd'  // Show the mean as a line (standard deviation)
        },
        {
          type: 'box',
          y: Object.values(data_json.opti_female_rendement),
          name: 'Female Directors',  // Female
          marker: {
            color: '#b56bea'
          },
          boxmean: 'sd'  // Show the mean as a line (standard deviation)
        }
      ];
  
      const layout = {
        title: 'Movie Rendement of the Optimal Group depending on Director Gender',
        xaxis: {
          title: 'Director Gender'
        },
        yaxis: {
          title: 'Movie Rendement'
        },
        showlegend: true
      };
  
      // Render the plot
      const Plotly = await import('plotly.js-dist');
      Plotly.newPlot(plotElement, data, layout);
    });
  </script>
  
  <div bind:this={plotElement}></div>
  