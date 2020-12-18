<script lang="coffeescript">

  import { createEventDispatcher, onMount } from "svelte"
  dispatch = createEventDispatcher()

  import TippyCss from "./Css.svelte"
  import tippy from 'tippy.js'

  mounted = false
  onMount ()->
    mounted = true

  export template = undefined
  export theme = "popover"

  # allow binding from parent

  export tippyObject = undefined
  export tippyComponent = undefined
  export tippyContent = undefined
  
  export style = undefined
  export classes = undefined
  export id = undefined



  export options = 
    theme: theme
    trigger: "click"
    placement: "bottom-end"
    interactive: true
    popperOptions:
      modifiers: [
        {
          name: "flip"
          options:
            fallbackPlacements: ["top","right","left"]
        }

      ]
    onCreate: (instance) ->
      tippyComponent = new tippyContent(target: instance.popper.querySelector('.tippy-content'))
      dispatch "create"
      tippyComponent.$on "tippy-event",  (e) ->
        console.log "POPOVER.svelte tippy event"
        console.log e.detail
        tippyObject.hide()
        dispatch e.detail.event, e.detail.value
      return      

    onHide: (instance)->
      dispatch "hide"

    onShow: (instance) ->
      dispatch "show"

    onUntrigger: (instance, event)->
      console.error "tippyjs untrigger"
      console.log event

  popover = (element, content) ->

    tippyContent = content
    
    unless (typeof content == 'function')
      options.content = content
    
    if Object.keys(options).length == 0
      tippyObject = tippy(element)
    else
      tippyObject = tippy(element, options)

    return
    {
      update: (params) ->
        console.error "update"
        dispatch "update"
        #if tippyComponent
        #  tippyComponent.$set { dateValue: newValue }

        return
      destroy: ->
        tippyObject.destroy()
        console.error "tippy destroy"
        dispatch "destroy"

    }

  


</script>

{#if mounted}
<div use:popover={template} {style} class={classes} {id}>
  <slot/> 
</div>
{/if}

