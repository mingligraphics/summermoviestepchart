<script>
    export let data;
    export let xScale;
    export let yScale;
    export let width;
    export let height;
  
    let tooltipWidth;

 
    $: x = xScale(data.time);
    $: y = yScale(data.revenue);
    
    const xNudge = 30;
    const yNudge = 30;
 
    $: xPosition = (tooltipWidth + x) > width ? (x - tooltipWidth - xNudge): (x + xNudge);
    $: yPosition = y;
 
    import { fly } from 'svelte/transition';

    $: sequel_name = data.name;

    $: xPosition_single = 1/6*width;
    $: yPosition_single = 1/5*height;

    $: sequel_revenue = Math.round(data.revenue / 1000000) + " million" ;
    const imageManagerId = data.imageManagerId;

 </script>
 
 {#if sequel_name != "Inside Out" && sequel_name != "Twister"}
 <div bind:clientWidth={tooltipWidth}
 class="tooltip" 
 transition:fly
 style="left: {xPosition}px; top: {yPosition}px">
 <h1>{data.sequel} <span>{data.time}</span></h1>
 <h2 class="movie_name">{data.name}</h2>
 <!-- <h2>Cumulative total: ${Math.round(data.revenue / 1000000)} million</h2> -->
 <!-- <span>{data.Downloads.toLocaleString()} downloads</span> -->
 </div>
{/if}
 {#if sequel_name == "Inside Out" || sequel_name == "Twister"}
 <div bind:clientWidth={tooltipWidth}
 class="tooltip" 
 transition:fly
 style="left: {xPosition_single}px; top: {yPosition_single}px">
 <h1 class="single">{sequel_name}</h1>
 <h2 class="single_revenue">Total box office: ${sequel_revenue}</h2>
 <!-- svelte-ignore a11y-missing-attribute -->
 <img width=250 height=250 src="https://images.wsj.net/im-{imageManagerId}"/>
 <!-- <span>{data.Downloads.toLocaleString()} downloads</span> -->
 </div>
 {/if}

 <style>
     .tooltip {
        position: absolute;
        background: white;
        box-shadow: 2px 3px 8px rgba(0, 0, 0, 0.15);
        padding: 8px 6px;
        border-radius: 3px;
        pointer-events: none;
        font-family: RetinaLight, sans-serif;
        transition: top 300ms ease, left 300ms ease;
        opacity: 0.8;
     }
 
 h1 {
     font-size: 1rem;
     font-weight: 600;
     margin-bottom: 4px;
     width: 100%;
 }
 
 h2 {
     font-size: 0.8rem;
     font-weight: 500;
     margin-bottom: 4px;
     /* text-transform: uppercase; */
 }
 
 span {
     background: #EFEFF0;
     font-size: 90%;
     padding: 2px 4px;
     display: inline-block;
     vertical-align: bottom;
     border-radius: 3px;
     color: rgba(0, 0, 0, 0.7);
     font-weight: 500;
 }

 .movie_name{
    color: #EABC28;
    font-weight: 600;
 }
 </style>
 