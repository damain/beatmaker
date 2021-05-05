<script>
    export var pad = {name:"", file:"", code:"", sequence:[]}
    export let beat=0
    export let settings = {muted:false}
    let audio = new Audio()
    let playing = ""
    let handleKeypress = (e)=>{
        if (e.key=== pad.code){
            console.log(e.key +" pressed")
            playInstrument()
        }
    }

    let playInstrument = ()=>{
        audio.currentTime = 0
        playing = "playing"
        audio.play()
    }

    let handleClick = ()=>{
        console.log(pad.name + "clicked")
        playInstrument()
    }

    let handleEnded = ()=>{
        playing = ""
    }

    $: if (pad.sequence.length>beat && pad.sequence[beat]==1){
        playInstrument()
    }
    
    $: if (audio.muted !== settings.muted) audio.muted = settings.muted
</script>
<svelte:window on:keypress={handleKeypress}></svelte:window>
<div class={"pad " + pad.name + " " + playing} on:click={handleClick}> {pad.name}
    <img src={pad.image} alt="" class="icon">
</div>
<audio bind:this={audio} src={pad.file} on:ended={handleEnded} preload="auto">
    <track kind="captions"/>
</audio>
<style>
    .pad {
        text-transform: capitalize;
        height: 90px;
        width: 100%;
        line-height: 90px;
        background-color: rgb(235, 235, 235);
        text-align: center;
        display: inline-block;
        vertical-align: middle;
        transition: all 0.2s ease-in-out;
        color: rgb(80, 80, 79);
        box-shadow: 2px 2px 3px 1px rgb(177, 177, 177) ;
        border-radius: 5px;
        transition: all .15s;
        -webkit-user-select: none;
        -moz-user-select: none;
      }
      .playing {
        background-color: rgb(125, 194, 240);
        box-shadow: 0px 0px 1px 0px rgb(139, 139, 139) ;
      }
      .icon{
        
          width: 30px;
      }
</style>