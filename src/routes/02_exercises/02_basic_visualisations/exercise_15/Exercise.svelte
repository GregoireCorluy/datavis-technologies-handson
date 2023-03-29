<script>
  const width = 100;
  const height = 100;
  const margin = { top: 5, right: 5, bottom: 5, left: 5 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;

  const size_rect = 40;
  const size_circ = 20;
</script>

<svg {width} {height}>
  <g transform="translate({margin.left}, {margin.top})">
    <!--  -->
    <rect x={(innerWidth-size_rect)/2} y={(innerHeight-size_rect)/2} width={size_rect} height={size_rect}/>
    
  
  </g>
  
  <!-- don't know if it has to be inside the group-->
  <circle cx={width-size_circ} cy={height-size_circ} r={size_circ} />
  
</svg>

<style>
  svg {
    border: 1px solid black;
    border-radius: 5px;
  }

  rect{
    fill: yellow;
  }

  circle{
    fill: skyblue;
  }
</style>

  