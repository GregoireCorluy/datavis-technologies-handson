<script>
    // Dimensions
    const width = 600;
    const height = 300;
    const margin = { top: 10, right: 10, bottom: 30, left: 60 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const data = [
      { service: "Netflix", viewers: 2.9 },
      { service: "Amazon Prime Video", viewers: 1.3 },
      { service: "Disney+", viewers: 2.1 },
      { service: "Hulu", viewers: 0.9 },
      { service: "Apple TV", viewers: 1.1 },
      { service: "Rakuten", viewers: 0.4 }
    ];

    import {axisBottom, axisLeft} from "d3-axis";
    import {scaleLinear} from "d3-scale";
    import {select} from "d3-selection";
    import {schemeDark2} from "d3-scale-chromatic";

    const xScale = scaleLinear().domain([0,3]).range([0,innerWidth]);

    const yScale = scaleLinear().domain([0,3]).range([0,0.9*innerHeight]);
    const yScaleInverse = scaleLinear().domain([3,0]).range([0,0.9*innerHeight]);

    const xAxis = axisBottom(xScale).tickValues([]);

    const yAxis = axisLeft(yScaleInverse).ticks(numberYTicks);

    function addAxisX(handle){
      xAxis(select(handle));

    }

    function addAxisY(handle){
      yAxis(select(handle));

    }

    const barWidth = 50;
    const barSpace = 80;

    const numberYTicks = 5;

    //const myColor = "red";

  </script>

  <!-- setting a viewBox and max-width allows the SVG to shrink but not grow! -->
  <svg viewbox="0 0 {width} {height}" style="max-width: {width}px" >
    <g transform="translate(10,0)">
      <g transform={`translate(${margin.left},${margin.top})`} >
        {#each data as point,index}
          <!--<rect x="20" y="50" height="50" width={barWidth} fill="red" />-->
            <rect x={0.1*margin.left+index*barSpace} y={margin.top + 0.9*innerHeight-yScale(point.viewers)-10} height={yScale(point.viewers)} width={barWidth} fill={schemeDark2[index]} />
            <text class="label" fill = "currentcolor" text-anchor="end" transform=" translate({0.1*margin.left+index*barSpace+barWidth*0.8},{0.9*innerHeight + 10}) rotate(-45)">
              {#if point.service.length>10}
                <tspan x="0" dy="0em">{point.service.slice(0, 10)}</tspan>
                <tspan x="0" dy="1.2em">{point.service.slice(10)}</tspan>
              {:else}
                {point.service}
              {/if}
            </text>
        {/each}
      </g>

      <g transform="translate({0.5*margin.left},{margin.top + 0.9*innerHeight})" use:addAxisX>
        <!--<text  fill = "currentcolor" text-anchor="end" transform=" translate(0,30) rotate(-45)"> test </text>-->

      </g>

      <g class="yLabel" transform="translate({0.5*margin.left},{margin.top})" use:addAxisY>
        <text font-size= "1.3em" fill = "currentcolor" text-anchor="middle" transform="translate({-0.5*margin.left},{innerHeight/2}) rotate(-90)"> Number of viewers </text>
      </g>

  </g>
  </svg>

  

  <style>
    /*svg{
      border: 1px solid black;
    }*/

    .label{
      font-size: 0.7em;
      font-weight: bold;
    }

    .yLabel{
      font-size:0.7em;
      font-weight: bold;
    }

  </style>
  