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
    $: sequel_revenue = data[data.length - 1].revenue / 1000000 > 1000 
    ? Math.round(data[data.length - 1].revenue / 1000000000 * 10) / 10 + " billion" 
    : Math.round(data[data.length - 1].revenue / 1000000) + " million" ;
    const imageManagerId = data[0].imageManagerId;
 </script>
 
 <div bind:clientWidth={tooltipWidth}
 class="tooltip" 
 transition:fly
 style="left: {xPosition}px; top: {yPosition}px">
 <h1>{sequel_name}</h1>
 <h2>Total box office: <span>${sequel_revenue}</span></h2>
 <!-- svelte-ignore a11y-missing-attribute -->
 <img width=250 height=250 src="https://images.wsj.net/im-{imageManagerId}"/>
 <!-- <span>{data.Downloads.toLocaleString()} downloads</span> -->
 </div>
 
 <style>
     .tooltip {
        position: absolute;
        background: white;
        box-shadow: 2px 3px 8px rgba(0, 0, 0, 0.15);
        padding: 6px 4px;
        border-radius: 3px;
        pointer-events: none;
        font-family: RetinaLight, sans-serif;
        transition: top 300ms ease, left 300ms ease;
        opacity: 0.8;
     }
 
 h1 {
     font-size: 1rem;
     font-weight: 600;
     margin-bottom: 2px;
     width: 100%;
 }
 
 h2 {
     font-size: 0.8rem;
     font-weight: 500;
     /* text-transform: uppercase; */
 }
 
 </style>
 