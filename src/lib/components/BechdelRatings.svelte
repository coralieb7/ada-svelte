<script>
    import { onMount } from 'svelte';
  
    let plotElement;
  
    onMount(async () => {
      // Load the data from the JSON file
      const response = await fetch('src/lib/json/bechdel_ratings.json');
      const data_json = await response.json();
  
      var traces1 = {
        x: Object.keys(data_json.male_director),
        y: Object.values(data_json.male_director),
        name: "Male Directors",
        type: 'bar'
        };
      var traces2 = {
        x: Object.keys(data_json.female_director),
        y: Object.values(data_json.female_director),
        name: "Female Directors",
        type: 'bar'
        };
      var data = [traces2, traces1];
      var layout = {
        barmode: 'group',
        title: 'Bechdel Test Ratings by Director Gender',
        xaxis: { title: 'Rating' },
        yaxis: { title: 'Percentage %' },
        template: 'plotly_white'
      };
  
      // Render the plot
      const Plotly = await import('plotly.js-dist');
      Plotly.newPlot(plotElement, data, layout);
    });
  </script>
  
  <div bind:this={plotElement}></div>
  