<script lang="coffeescript">

  import { createEventDispatcher, onMount } from "svelte"
  dispatch = createEventDispatcher()

  import TippyCss from "./Css.svelte"
  import tippy from 'tippy.js'

  mounted = false
  onMount ()->
    mounted = true

  export template = undefined
  export theme = "context-menu"

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
    placement: "right-start"
    interactive: true
    offset: [0,0]
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
        # console.log 'tippy-event'1
        # console.log e.detail
        tippyObject.hide()
        dispatch e.detail.event, e.detail.value
      return      

    onHide: (instance)->
      # tippyObject.destroy()
      dispatch "hide"


    onShow: (instance) ->
      dispatch "show"


  popover = (element, content) ->
    tippyContent = content


    unless (typeof content == 'function')

      options.content = content
    
    if Object.keys(options).length == 0
      tippyObject = tippy(element)
    else
      tippyObject = tippy(element, options)


    element.addEventListener "click", (event)->
      tippyObject.setProps 
        getReferenceClientRect: () ->
          return {
            height: 0
            top: event.clientY
            bottom: event.clientY
            left: event.clientX
            right: event.clientX
          }
      tippyObject.show()

    return
    {
      update: (params) ->
        console.error "update"
        dispatch "update"
        #if tippyComponent
        #  tippyComponent.$set { dateValue: newValue }

        return
      destroy: ->
        # tippyObject.destroy()
        console.error "tippy destroy"
        dispatch "destroy"

    }

  


</script>

{#if mounted}
<div use:popover={template} {style} class={classes} {id}>
  <slot/> 
</div>
{/if}

