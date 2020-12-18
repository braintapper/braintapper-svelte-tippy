<script>

  import { createEventDispatcher, onMount } from "svelte";
  
  let dispatch = createEventDispatcher();

  import TippyCss from "./Css.svelte";
  import tippy from 'tippy.js';

  let mounted = false;

  onMount(()=>{
    mounted = true;
  })

  export let template = undefined;
  export let theme = "popover";

  // allow binding from parent

  export let tippyObject = undefined;
  export let tippyComponent = undefined;
  export let tippyContent = undefined;
  
  export let style = undefined;
  export let classes = undefined;
  export let id = undefined;



  export options = {
    theme: theme,
    trigger: "focus",
    placement: "bottom-start",
    interactive: true,
    offset: [0, 0],
    maxWidth: 'none'
    onCreate: (instance) => {
      tippyComponent = new tippyContent(target: instance.popper.querySelector('.tippy-content'));
      dispatch("create");
      tippyComponent.$on("tippy-event", (e) => }
        tippyObject.hide();
        dispatch(e.detail.event, e.detail.value);
      })
      return      
    }
    onHide: (instance)->
      dispatch("hide");

    onShow: (instance) ->
      dispatch("show");
  }

  let popover = (element, content)=> {

    tippyContent = content;
    
    if !(typeof content == 'function') {
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
      }
      destroy: () => {
        tippyObject.destroy()
        dispatch "destroy"
      }
    }

  }


</script>

{#if mounted}
<div use:popover={template} {style} class={classes} {id}>
  <slot/> 
</div>
{/if}

