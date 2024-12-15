<script>
    import Sortable from 'sortablejs';
    import { onMount } from "svelte";
  
    let el;
  
    onMount(() => {
      if (el) {
        Sortable.create(el, { /* your sortable options here */ });
      }
    });
  </script>
  
  <ul bind:this={el}>
    <li>Reorder Me</li>
    <li>And me!</li>
  </ul>
  