<script>
  import {onMount} from 'svelte';

  // Properties
  export let data = [];
  const continents = ["europe", "asia", "americas", "africa"];

  let play = true;
  let increase_delta = 1;
  $: text_button = ((play) ? "Pause" : "Play");
  $: increase = ((play) ? increase_delta : 0);

  let reset_variable = false;
  //let text_button = "Pause";

  const year_base = 1800;
  const max_year_increase = 214;
  export let value_year = 0;
  export let selected_continent;
  //let increase=1;

  function play_pause(){

    play = !play;

    /*if(play){
      increase = 1;
    }
    else if(!play){
      increase = 0;
    }*/
  }

  function reset_button(){
    play = false;
    value_year = 0;
    //increase = 0;
  }

  let my_interval;

    onMount(() => {
      my_interval = setInterval(update_slider, 100);
    });

  function update_slider(){
    value_year = value_year+increase;
    
    if(value_year>max_year_increase){
      value_year=0;
    }
  }
  

</script>

<div class="row">
  <!--  -->
  <button on:click={play_pause} >
    {text_button}
  </button>
  
  <button on:click={reset_button} >
    Reset
  </button>
  <br/>
  <input type=range bind:value={value_year} min=0 max={max_year_increase}>
  <label>Year: {year_base+value_year}</label>
  <br/>
  <select bind:value={selected_continent} on:change>
		{#each continents as continent}
			<option value={continent}>
				{continent}
			</option>
		{/each}
	</select>
  </div>
 

<style>
button{
  width:100px;
  border-radius: 20px;
  margin-left: 20px;
}
input{
  margin-left: 20px;
  margin-right: 20px;
  margin: 20px;
  max-width: 350px;
}
label{
  margin-left: 10px;
  margin-top: -15px;
}
select{
  margin-top: 10px;
  margin-left:20px;
  max-width: 120px;
}

</style>