<script>
  import { json } from "d3-fetch";
  import { onMount } from "svelte";

  import Controls from "./Controls.svelte";
  import Scatterplot from "./Scatterplot.svelte";

  
  let selected_continent_ex='europe';
  let selected_year=0;

  
  // Load the data
  let data = null;
  onMount(async () => {
    data = await json("/data/gapminder.json");
    
  });

  $: selected_data = data ? data[selected_year]['countries'].filter(e => e["continent"]==selected_continent_ex):[];

</script>

{#if !data}
  <p>Loading the data, please wait...</p>
{:else}
  <div>
    <Scatterplot data={selected_data} />
    <Controls bind:selected_continent={selected_continent_ex} bind:value_year={selected_year} {data} />
  </div>
{/if}
