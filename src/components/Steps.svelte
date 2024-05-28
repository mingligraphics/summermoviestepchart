<script>
    export let currentStep;
    import Scrolly from "../helpers/Scrolly.svelte";

    $: steps = [
    // 0 
    `<p>It’s the summer of the sequel, with Hollywood returning to popular franchises for box office success.</p>`,
    `Illumination and Universal’s ‘Despicable Me’ and Minions movies have proved to be consistent hits, grossing a collective $1.6 billion since 2010`,
    // 2 
    `Disney’s Pixar, which has had success with sequels in its ‘Toy Story’ franchise, is slated to release ‘Inside Out 2’ in June.`,
    `Sony’s planned release of ‘Bad Boys: Ride or Die’ marks the continuation of a long-running franchise starring Will Smith and Martin Lawrence.`,
    `Note: U.S. and Canada ticket sales<br>Source: Comscore`
  ];
</script>
<div class="steps">
    <Scrolly bind:value={currentStep}>
      {#each steps as text, i}
      <div class="step" class:active={currentStep === i}>
        <div class="step-content">
          {@html text}
        </div>
      </div>
      {/each}
    </Scrolly>
  </div>

  <style>
    .step {
    height: 90vh;
    opacity: 0.3;
    transition: opacity 300ms ease;

/* vertically and horizontally center the steps */
    display: flex;
    justify-content: center;
    place-items: center;

}

.step-content {
  position: relative;
  box-sizing: border-box;
  z-index: 1;
  -webkit-transform: translate3d(0, 0, 0); /*for safari z-index issue*/
  height: auto;
  width: 100%;
  max-width: 700px; 
  margin: 0 auto;
  font-family: RetinaLight, sans-serif;
  font-size: 17px;
  line-height: 27px;
  font-weight: 400;
  color: #333;
  padding: 20px 25px 20px;
  box-shadow: 0 0 1px 0 rgba(0, 0, 0, .4);
  overflow: visible;
  background-color: rgba(255, 255, 255, .9);
}

.step.active {
  opacity: 1;
}

.steps {
  position: relative;
  z-index: 2;
  pointer-events: none;
}

/* mark{
  padding-top: 3px;
  padding-bottom: 3px;
  padding-left: 4px;
  padding-right: 4px;
  margin-right: 1px;
  margin-left: 1px;
  border-radius: 4px;
  white-space: nowrap;
  font-weight: 500;
  text-shadow: none;
} */
  </style>