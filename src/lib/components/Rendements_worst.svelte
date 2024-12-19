<script>
    import { onMount } from 'svelte';
  
    let plotElement;
  
    onMount(async () => {
        const response = await fetch('/json/opti_vs_worst_rendement.json');
        const data_json = await response.json();
  
      const data = [
        {
          type: 'box',
          y: Object.values(data_json.worst_male_rendement),
          name: 'Male Directors',  // Male
          marker: {
            color: '#2D9884'
          },
          boxmean: 'sd'  // Show the mean as a line (standard deviation)
        },
        {
          type: 'box',
          y: Object.values(data_json.worst_female_rendement),
          name: 'Female Directors',  // Female
          marker: {
            color: '#c48bf0'
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
  