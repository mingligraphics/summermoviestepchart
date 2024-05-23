<script>
    export let xScale;
    export let xTicks;
    export let height;
    export let margin;
    export let width;
    
    </script>
    
    <g class="axis x-axis">
        {#each xTicks as tick, i}
          <g class="tick tick-{tick}" transform="translate({xScale(tick) + margin.left},{margin.top})">
            <line x1="0" x2="0" y1="0" y2={height} stroke="#dcddde" stroke-width=1/>
            <text x=-2 y={-25} dx={-10} dy="20">{tick}</text>
          </g>
        {/each}
        <text x={3/5 * width } y={20}
        dy="0"
        dominant-baseline="start"
        text-anchor= "end"
        class = "axis-title"
        >Release year</text>
    </g>
    
    <style>
    
    </style>