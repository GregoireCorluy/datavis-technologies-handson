<script>
    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 20, right: 5, bottom: 5, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [
      { x: 2, y: 1, category: "cat1" },
      { x: 4, y: 2, category: "cat3" },
      { x: 6, y: 1, category: "cat2" },
      { x: 7, y: 3, category: "cat3" },
      { x: 9, y: 1, category: "cat2" }
    ];

    import {scaleLinear, scaleOrdinal} from "d3-scale";
    import {schemeCategory10} from "d3-scale-chromatic"

    const scaleCircle = scaleLinear()
        .domain([values[0].x-1,values[values.length-1].x+1]) //+1 and -1 to have everything inside and not at the edge
        .range([innerWidth, innerHeight]);

    const radius = 10;

    function findMax(array){
      let maxVal = Number.MIN_VALUE;

      //not good in the javascript section
      /*{#each array as val}
        {if val.x>max}
          max = val.max;
        {/if}
      {/each}*/

      for (var i = 0; i < array.length; i++){
          if(array[i].y>maxVal){
              maxVal = array[i].y;
          }
      }

      return maxVal;
    }

    const categories = Array.from(Array(findMax(values)).keys()).map(v=> v+1); //.map shift every value with one

    const colorScale = scaleOrdinal().domain(categories).range(schemeCategory10.slice(0,categories[categories.length-1]));
  </script>
  
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})">
      <!--  -->
      {#each values as val}
        <text class="valueLabel" x={scaleCircle(val.x)}  y={innerHeight/2-10-radius}> {val.y} </text>
        <circle fill={colorScale(val.y)} cx={scaleCircle(val.x)}  cy={innerHeight/2}   r = {radius} />
        {scaleCircle(val.x)}
        <line x1={scaleCircle(val.x)} y1={innerHeight} x2={scaleCircle(val.x)} y2={innerHeight/2} stroke={colorScale(val.y)} stroke-width="2" stroke-opacity="0.75" stroke-linecap="round"/>
      {/each}
    </g>
  </svg>
  
  <style>
    text {
      text-anchor: middle;
      font-size: small;
    }
  </style>
  