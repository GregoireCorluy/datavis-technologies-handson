<script>
  // Properties
  export let data = [];
  const continents = ["europe", "asia", "americas", "africa"];

  let play = false;
  $: text_button = ((play) ? "Play" : "Pause");
  //let text_button = "Pause";

  const year_base = 1800;
  let value_year = 0;
  let selected_continent;

  function play_pause(){

    play = !play;
  }

  function reset_function(){


  }

</script>

<div class="row">
  <!--  -->
  <button on:click={play_pause} >
    {text_button}
  </button>
  <br/>
  <button on:click={reset_function} >
    Reset
  </button>
  <br/>
  <input type=range bind:value={value_year} min=0 max=100>
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