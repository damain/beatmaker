<script>
  import { createEventDispatcher } from "svelte";
  export let lit = false;
  export let beat = 0;
  export let index = 0;
  export let name = "test";
  const dispatch = createEventDispatcher();
  let handleClick = () => {
    dispatch("lightClicked", { index, lit });
  };

  let hovered = false;
</script>

<div
  class={"light " + (lit ? "lit " : "unlit ") + (beat === index ? "highlight" : "unhilighted")}
  on:click={handleClick}
  on:mouseenter={() => {
    hovered = true;
  }}
  on:mouseleave={()=>{hovered = false}}
>
  {hovered?name:""}
</div>

<style>
  .unlit {
    background-color: rgb(252, 245, 238);
  }
  .lit {
    background-color: tomato;
  }
  .light {
    transition: all 200ms;
    width: 100%;
    height: 30px;
    /* border: 1px solid white; */
    text-align: center;
    overflow-x: hidden;
    border-radius:3px;
    box-shadow: 0px 0px 2px 0px rgb(151, 151, 151);
    
  }
  .light.highlight {
    /* border: 1px solid rgb(93, 183, 243); */
    background-color: palegreen;
    /* box-shadow: 0px 5px 5px 3px rgba(75, 159, 255, .3) ; */
  }
  .light.highlight.lit{
    background-color: powderblue;
  }
</style>
