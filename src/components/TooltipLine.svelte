<script>
    export let data;
    export let width;
    export let height;
  
    let tooltipWidth;
    
    const xNudge = 30;
    const yNudge = 30;
 
    $: xPosition = 1/6*width;
    $: yPosition = 1/5*height;
 
    import { fly } from 'svelte/transition';

    const sequel_name = data[0].sequel;
    const sequel_revenue = data[data.length - 1].revenue;
 </script>
 
 <div bind:clientWidth={tooltipWidth}
 class="tooltip" 
 transition:fly
 style="left: {xPosition}px; top: {yPosition}px">
 <h1>{sequel_name}</h1>
 
 <h2>Total box office: <span>${Math.round(sequel_revenue / 1000000)} million</span></h2>
 <!-- <span>{data.Downloads.toLocaleString()} downloads</span> -->
 </div>
 
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
     font-size: 2.5rem;
     font-weight: 600;
     margin-bottom: 4px;
     width: 100%;
 }
 
 h2 {
     font-size: 1.5rem;
     font-weight: 500;
     /* text-transform: uppercase; */
 }
 
 </style>
 