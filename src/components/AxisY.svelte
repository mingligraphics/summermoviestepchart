<script>
    export let yScale;
    export let yTicks;
    export let margin; 
</script>
    
<g class="axis y-axis">
  {#each yTicks as tick, i}
   <g
    class="tick tick-{tick}"
    transform="translate(0 {yScale(tick)})">
    <line 
    x1={0} 
    y1={margin.bottom + 30 }
    x2={i === 7 ? 65 : 30} 
    y2={margin.bottom + 30}
    stroke={i === 0 ? "#333333" : "#e5e7eb"}/>
    <text x={i === 0 ? 5 : i === 8 ? 0 : 5} y={margin.bottom + 25}>{i == 7 ? "$" : ""}{i == 0 ? "0" : (tick / 1000000000).toFixed(1)}{i == 7 ? " billion" : ""}</text>
  </g>
  {/each}
</g>
        
<style>
        
</style>