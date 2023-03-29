<script>
  // Dimensions
  const width = 800;
  const height = 100;
  const margin = { top: 5, right: 5, bottom: 5, left: 5 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;

  const radius = 10;
  const radiusSmall = 2;

  // Array
  const values = [2, 4, 6, 7, 9];

  import {scaleLog} from "d3-scale";

  const myScale = scaleLog().domain([values.sort()[0],values.sort()[values.length-1]]).range([radius,innerWidth-radius]);
</script>



<svg viewBox="0 0 {width} {height}">
  <g transform="translate({margin.left},{margin.top})">
    <!--  -->
    {#each values as val}
      <circle style="fill:red;" cx={myScale(val)} cy = {innerHeight/2} r = {radius}/>
      <circle style="fill:green;" cx={myScale(val)} cy = {innerHeight/2} r = {radiusSmall}/>
      
      
      {/each}
  </g>
</svg>