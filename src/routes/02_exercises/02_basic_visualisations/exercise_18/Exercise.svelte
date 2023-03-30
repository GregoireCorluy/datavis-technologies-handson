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
  import {axisBottom} from "d3-axis";
  import {select} from "d3-selection";



  const myScale = scaleLog().domain([values.sort()[0],values.sort()[values.length-1]]).range([radius,innerWidth-radius]);
  const xAxis = axisBottom(myScale);

  function addAxis(handle){
    xAxis(select(handle))
  }

</script>



<svg viewBox="0 0 {width} {height}">
  <g transform="translate({margin.left},{margin.top})">
    <!--  -->
    {#each values as val}
      <circle style="fill:red;" cx={myScale(val)} cy = {innerHeight/2} r = {radius}/>
      <circle style="fill:green;" cx={myScale(val)} cy = {innerHeight/2} r = {radiusSmall}/>      
    {/each}
  </g>

  <g transform="translate({margin.left},{margin.top+0.8*innerHeight})" use:addAxis>
      <text fill = "currentcolor" font-size=20px x={innerWidth/2} y={(0.2*innerHeight)}> x-axis </text>
  </g>
  
</svg>

