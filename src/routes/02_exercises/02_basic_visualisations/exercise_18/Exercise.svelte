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

  function myFunction(handle){
    console.log('call axis')
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

  
  <g transform="translate({margin.left+50},{margin.top+50})" use:myFunction>
    <circle cx=100 cy=10 r=10 />
    <!--axisBottom(myScale)-->
    <!--{xAxis(select(handle))}-->
    xAxis(select(handle))
    <g transform="translate({innerWidth/2},0)">
      <text> x-axis </text>
    </g>
  </g>

  <!--svg.append("g")
            .attr("transform", "translate({margin.left+10},{margin.top+10})")
            .call(xAxis)-->


  <!--{xAxis}-->

  <!--
  <svg x="0" y={margin.top+innerWidth/2} height={innerHeight/2} width={innerWidth}>
    
    <circle style="fill:red;" cx={100} cy = {innerHeight/2} r = {radius}/>
    <g transform="translate({margin.left},{margin.top+innerWidth})">
      {xAxis}
    </g>
  </svg>
  -->
  
</svg>

<style>
  svg {
    border: 1px solid black;
    border-radius: 5px;
  }
</style>