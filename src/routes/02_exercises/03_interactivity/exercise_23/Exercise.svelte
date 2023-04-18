<script>
  import {onMount} from 'svelte';
  
    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 10, right: 20, bottom: 20, left: 20 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Arrays
    const points = [
      innerWidth / 2 - 60,
      innerWidth / 2 - 30,
      innerWidth / 2,
      innerWidth / 2 + 30,
      innerWidth / 2 + 60
    ];

    let radius = 10;

    let counter = 0;
  
    // All lights with a higher index are on!
    let max_index = points.length;
  
    // Color
    let color_off = "darkred"; //darkred
    let color_transition = "red";
    let color_on = "lime";

    let opacity_off = 0.3;
    let opacity_on = 1;

    let my_interval;

    onMount(() => {
      my_interval = setInterval(update_lights, 1000);
    });

    /*function set_color(){
      if(counter>max_index){
      return color_on
    }
      return color_transition;
    }
  function set_opacity(index){
    if(index<counter){
      return opacity_on;
    }
    else if(counter>max_index){
      return opacity_on;
    }
    else{
      return opacity_off;
    }
  }*/

  $: color = (counter > max_index) ? color_on : color_transition;

  $: opacity = (index) => {
    if (index < counter || counter > max_index) {
      return opacity_on;
    } else {
      return opacity_off;
    }
  }

  function update_lights(){
    counter= counter+1;
  }
  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      <!--  -->
      {#each points as point, index}
        <circle cx={point} cy={innerHeight/2} r={radius} fill={color} opacity={opacity(index)}/>
      {/each}
    </g>
    
  </svg>
  The counter is equal to {counter}.
  