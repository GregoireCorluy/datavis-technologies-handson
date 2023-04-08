<script>
  export let data_scatter;
  export let loaded_scatter;

  import {scaleLinear, scaleLog, scaleOrdinal} from 'd3-scale';
  import {schemeSet1} from "d3-scale-chromatic";
  import {axisBottom, axisLeft} from "d3-axis";
  import {select} from "d3-selection";

  // Dimensions
  const [height, width] = [400, 600];
  const margin = { top: 50, right: 5, bottom: 55, left: 50 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;

  const min_income = findMin(data_scatter,"income");
  const min_life_exp = findMin(data_scatter,"life_exp");
  const min_population = findMinGreaterZero(data_scatter,"population");

  const max_income = findMax(data_scatter,"income");
  const max_life_exp = findMax(data_scatter,"life_exp");
  const max_population = findMax(data_scatter,"population");

  const max_radius = 20;

  const font_size_title = 25;
  const font_size_label = 18;

  //income has an exponential distribution, therefore use a logaritmic scale to compress the high values
  const xScale = scaleLog().domain([min_income,max_income]).range([0,innerWidth]);
  const yScale = scaleLinear().domain([min_life_exp,max_life_exp]).range([innerHeight,0]); //y axis is inverted
  const radiusScale = scaleLinear().domain([min_population,max_population]).range([2,max_radius]);

  function findMax(array, key){
      let maxVal = Number.MIN_VALUE;

      for (var i = 0; i < array.length; i++){
          if(array[i][key]>maxVal){
              maxVal = array[i][key];
          }
      }

      return maxVal;
    }

    function findMin(array, key){
      let minVal = Number.MAX_VALUE;

      for (var i = 0; i < array.length; i++){
          if(array[i][key]<minVal && array[i][key]!=null){
            minVal = array[i][key];
          }
      }

      return minVal;
    }

    function findMinGreaterZero(array, key){ //find minimal value above zero
      let minVal = Number.MAX_VALUE;

      for (var i = 0; i < array.length; i++){
          if(array[i][key]<minVal && array[i][key]!=null && array[i][key]>0){
            minVal = array[i][key];
          }
      }

      return minVal;
    }

    function findCategories(data,key){
      let categories = [];
      
      for(var i=0;i<data.length;i++){
        if(!categories.includes(data[i][key])){
          categories.push(data[i][key]);
        }
      }

      return categories;
    }


    const continents = findCategories(data_scatter,'continent');

    const colorScale = scaleOrdinal().domain(continents).range(schemeSet1.slice(0,continents.length-1));
    
    const numberXTicks = 10;
    const numberYTicks = 10;

    //axis
    const xAxis = axisBottom(xScale).ticks(numberXTicks);

    const yAxis = axisLeft(yScale).ticks(numberYTicks);

    function addAxisX(handle){
      xAxis(select(handle));

    }

    function addAxisY(handle){
      yAxis(select(handle));

    }

    //actions when circle is hovered
    let hovered = false;
    let hoveredDatapoint = null;

    function handleMouseOver(datapoint) {
		  hovered = true;
      hoveredDatapoint = datapoint;
	  }
	  function handleMouseOut(e) {
		  hovered = false;
      hoveredDatapoint = null;
	  }

    //better to concatenate it in an array
    const startLegendX = 420;
    const startLegendY = 100;
    const widthLegend = 125;
    const heightLegend = 175;
    const yLegendMargin = 0.25*heightLegend;
    const yLegendSpace = 0.25*heightLegend;
    const radiusLegend = 15;

</script>

<svg viewBox="0 0 {width} {height}" style="max-width: {width}px">
  <g transform="translate({margin.left}, {margin.top})">
    <!--  -->

    <!-- legend that appears when a circle is hovered-->
    <!-- even better would be to add the flag of the country -->
    {#if hovered}
      <rect id="legend" x={startLegendX} y={startLegendY} width={widthLegend} height={heightLegend} rx={radiusLegend} />
      <text class="text_legend" fill="currentcolor"  x={startLegendX+0.5*widthLegend} y={startLegendY + yLegendMargin} >
         {#if hoveredDatapoint.country.length>10}
              <tspan x={startLegendX+0.5*widthLegend} dy="0em">{hoveredDatapoint.country.slice(0, 10)}</tspan>
              <tspan x={startLegendX+0.5*widthLegend} dy="1.2em">{hoveredDatapoint.country.slice(10)}</tspan>
            {:else}
              {hoveredDatapoint.country}
          {/if}
        </text>
      <text class="text_legend" fill="currentcolor"  x={startLegendX+0.5*widthLegend} y={startLegendY + yLegendMargin + yLegendSpace}> Life exp.: {hoveredDatapoint.life_exp}</text>
      <text class="text_legend" fill="currentcolor"  x={startLegendX+0.5*widthLegend} y={startLegendY + yLegendMargin + 2*yLegendSpace}> Income: {hoveredDatapoint.income}</text>
      {/if}
    
    <!-- plot all the points-->
    {#each data_scatter as datapoint}
      {#if datapoint.income!=null && datapoint.life_exp!=null}
        <circle stroke = "black" style="fill:{colorScale(datapoint.continent)};" cx ={xScale(+datapoint.income)} cy={yScale(+datapoint.life_exp)} r={radiusScale(+datapoint.population)} on:mouseover={handleMouseOver(datapoint)} on:mouseout={handleMouseOut} />
        <!-- plus sign is added to the values to indicate that the values are numeric-->
      {/if}
    {/each}

    <!-- title and label below-->
    <text fill="currentcolor" style="color: #ff744a; font-size:{font_size_title}" x={innerWidth/2} y={-10-font_size_title*0.91}> Life expectancy in function of the income</text>
    <text fill="currentcolor" style="color: #289026; font-size:{font_size_label}" x={innerWidth/2} y=-10> Year 1800</text>
    <!-- to improve the interactivity, the user should be able to select the year that he wants at the location of the label and the data scatterplot would change-->


    <!-- add x and y axis with the labels-->
    <g transform="translate(0,{innerHeight})" use:addAxisX> <!-- {0.5*margin.left},{margin.top + 0.9*innerHeight}-->
      <text font-size= "1.3em" fill = "currentcolor" text-anchor="middle" transform="translate({innerWidth/2},{0.5*margin.bottom})"> Income </text>

    </g>

    <g class="yLabel" transform="translate(0,0)" use:addAxisY>
      <text font-size= "1.3em" fill = "currentcolor" text-anchor="middle" transform="translate({-0.5*margin.left},{innerHeight/2}) rotate(-90)"> Life expectancy </text>
    </g>

    
  </g>
</svg>

<style>
  svg g text{
    /*color: forestgreen;
    font-size: var(font_size)px;*/
    font-family: 'Playfair Display';
    font-weight: bold;
    text-anchor: middle;
  }


  circle{
    opacity:0.8; 
  }

  circle:hover{
    opacity:1;
    stroke: red;
    stroke-width: 2px;
  }

  #legend{
    stroke:black;
    stroke-width: 2px;
    fill: rgb(63,55,201);
    background-color: 3a0ca3;
  }

  .text_legend{
    text-anchor: middle;
    color: 03045e;
    font-weight: bold;
    font-family: "Arial";
    font-size: 17px;
    color: white;
  }

</style>
