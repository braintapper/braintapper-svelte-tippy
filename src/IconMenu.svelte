<script>

  import { createEventDispatcher, onMount } from "svelte";
  let dispatch = createEventDispatcher();

  import"./tippy.css";
  import tippy from 'tippy.js';

  let mounted = false;

  onMount(()=>{
    mounted = true;
  })


  
  export let template = undefined;
  export let theme = "menu";

  // allow binding from parent

  export let tippyObject = undefined;
  export let tippyComponent = undefined;
  export let tippyContent = undefined;
  
  export let style = undefined;
  export let classes = undefined;
  export let id = undefined;
  export let disabled = false;


  // export let events = {};

  export let options = {
    theme: theme,
    trigger: "click",
    placement: "bottom-end",
    interactive: true,
    popperOptions: {
      modifiers: [
        {
          name: "flip",
          options: {
            fallbackPlacements: ["top","right","left"]
          }
        }
      ]
    },
    onCreate: (instance) => {
      tippyComponent = new tippyContent({target: instance.popper.querySelector('.tippy-content')});
      dispatch("create");
      tippyComponent.$on("tippy-event", (e) => {
        tippyObject.hide();
        dispatch(e.detail.event, e.detail.value);
      })
      return      
    },
    onHide: (instance)=> {
      dispatch("hide");
    },
    onShow: (instance)=> {
      dispatch("show");
    }
  }

  let popover = (element, content)=> {

    tippyContent = content;
    
    if (typeof content != 'function') {
      options.content = content;
    }

    if (Object.keys(options).length == 0) {
      tippyObject = tippy(element)
    } else {
      tippyObject = tippy(element, options)
    }

    return {
      update: (params) => {
        console.error("update");
        dispatch("update");
        return
      },
      destroy: () => {
        tippyObject.destroy()
        dispatch("destroy");
      }
    }

  }


</script>

{#if mounted}
  <button type="button" on:click use:popover={template} {disabled} {style} class={classes} {id}><slot/></button>
{/if}

<style>
button {
  display: inline-block;
  padding: 0px;
  background: none;
  height: 24px;
  min-width: 24px;
  width: 24px;
  border: none;
  margin: 0px; }
  button:hover {
    background: none; }



</style>