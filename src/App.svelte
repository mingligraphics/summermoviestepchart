<script>
  import data from "./data/movie.json";
  import { extent, group} from "d3-array";
  import { scaleLinear } from "d3-scale";
  import {line, curveStep, curveNatural, curveStepAfter} from "d3-shape";
  import AxisX from "/components/AxisX.svelte";
  import AxisY from "/components/AxisY.svelte";
  import { timeFormat } from "d3-time-format";
  import Tooltip from "/components/Tooltip.svelte";
  import TooltipLine from "/components/TooltipLine.svelte";

  console.log(data)
  
  let initialData = data;
  // let renderedData = Object.groupBy(initialData, ({ sequel }) => sequel);
  let renderedData = group(initialData, (d) => d.sequel);
  let textLableData = initialData.filter(d => d.time === 2024)

  console.log(textLableData)
  
  const margin ={
    top: 50,
    right: 110,
    bottom: 20,
    left:100
  }

  $: width = 700;
  $: innerWidth = width - margin.left - margin.right;

  let height = 600;
  let innerHeight = height - margin.top - margin.bottom;

  $: extentX = extent(data, (d) => d.time);

  $: extentY = extent(data, (d) => d.revenue);

  $: xScale = scaleLinear()
    .domain(extentX)
    .range([0,innerWidth]);
  
  $: yScale = scaleLinear()
    .domain([0, extentY[1]])
    .range([innerHeight, 0]);

  $: pathLine = line()
	  .x((d) => xScale(d.time))
    .y((d) => yScale(d.revenue))
	  .curve(curveStepAfter);

  $: xTicks = xScale.ticks(8);
  $: yTicks = yScale.ticks(8);

  var formatTime_xaxis = timeFormat("%Y");
  let hoveredData;
  let hoveredLineData;
  let hoveredSequel;
  let hoveredClass = false;
  
</script>

<main>
<div class="chart-container" bind:clientWidth={width}>
  <h1>Select movie sequels in summer 2024</h1>
  <svg {width} {height}>
  <AxisX {xScale} {xTicks} {margin} {formatTime_xaxis} height = {innerHeight}/>
  <AxisY  {yTicks} {yScale} {width} {margin}/>
  <g transform="translate({margin.left} {margin.top})" on:mouseleave={()=>{hoveredLineData = null; hoveredData = null; hoveredSequel=null ; hoveredClass=false}}>
    {#each textLableData as label, i}
    <text
    class="sequel-lables"
    x={innerWidth + 10}
    y={i==1 ? yScale(label.revenue) + 15 : i==3 ? yScale(label.revenue) - 5 : yScale(label.revenue) + 5}
    style={'text-anchor:start'}
    font-weight={300}>
    {label.sequel}
    </text>
    {/each}
    {#each [...renderedData] as [key, value]}
    <path 
    fill="none"
    stroke={hoveredLineData == value || hoveredSequel == key ? "#EEC73A" : "#5AC5C2"}
    stroke-width={hoveredLineData == value || hoveredSequel == key ? 6 : 1.5}
    d={pathLine(value)}
    class:hoveredClass
    on:mouseover={()=>{
      hoveredLineData = value;
      hoveredSequel = key;
      hoveredClass = true;
      }}
    on:focus={()=>{
      hoveredLineData = value;
      hoveredSequel = key;
      hoveredClass = true;
      }}
    tabindex="0"
    role="tab"
    aria-roledescription="line"
    />
    {#each value as d}
      <circle
      cx={xScale(d.time)}
      cy={yScale(d.revenue)}
      class:hoveredClass
      r={hoveredData == d || hoveredSequel == d.sequel ? 8 : 4.5}
      fill={hoveredData == d || hoveredSequel == d.sequel ? "white" : "#EABC28"}
      opacity=1
      stroke={hoveredData == d ? "black" : hoveredSequel == d.sequel ? "#EEC73A" : "white"}
      stroke-width={hoveredData == d || hoveredSequel == d.sequel ? "4" : 1}
      on:mouseover={()=>{
        hoveredData = d;
        hoveredSequel = d.sequel;
        hoveredLineData = null;
        hoveredClass = true;
        }}
      on:focus={()=>{
        hoveredData = d;
        hoveredSequel = d.sequel;
        hoveredLineData = null;
        hoveredClass = true;
        }}
      tabindex="0"
      role="tab"
      aria-roledescription="circle"
      />
      {/each}
    {/each}
  </g>
  </svg>
  {#if hoveredLineData}
  <TooltipLine data={hoveredLineData} width = {innerWidth} height = {innerHeight}/>
  {/if}
  {#if hoveredData}
  <Tooltip data={hoveredData} {xScale} {yScale} width = {innerWidth}/>
  {/if}
 <p class="footnote">Source: Comscore</p>
</div>
</main>

<style>
   :global(.tick text, .axis-title){
      fill: #666;
      text-anchor: start;
      font-family: RetinaNarrowLight,  sans-serif;
      font-size: 13px;
      line-height: 15.6px;
    }

    :global(.axis-title){
        line-height: 13px;
    }

  main{
  max-width: 700px;
  margin:0 auto;
}

h1{
    color: #333333;
    font-family: Retina, sans-serif;
    font-size: 15px;
    font-weight: 500;
    margin-bottom:4px;
    line-height: 20px;
    }

  /* .chart-container {
  height:100%;
  width:100%;
  max-width: 700px;
  max-height: 550px;
} */

.hoveredClass {
  z-index: 999;
}

.sequel-lables{
    color: #333333;
    font-family: Retina, sans-serif;
    font-size: 15px;
  }

  .footnote{
    color: #727272;
    font-weight: 300;
    font-family: Retina, sans-serif;
    font-size: 13px;
    line-height: 17px;
    margin-top:4px;
  }

</style>