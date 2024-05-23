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
    stroke={"#e5e7eb"}/>
    <text x={i === 0 ? 5 : i === 8 ? 0 : 5} y={margin.bottom + 25}>{i == 7 ? "$" : ""}{tick / 1000000000}{i == 7 ? " billion" : ""}</text>
  </g>
  {/each}
</g>
        
<style>
        
</style>