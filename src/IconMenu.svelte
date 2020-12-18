<script lang="coffeescript">

  import { createEventDispatcher, onMount } from 'svelte'
  dispatch = createEventDispatcher()

  import TippyCss from "./Css.svelte"
  import tippy from 'tippy.js'

  mounted = false
  onMount ()->
    mounted = true

  
  export template = undefined  # svelte template for the popover
  export theme = "menu"


  # allow binding from parent

  export tippyObject = undefined
  export tippyComponent = undefined
  export tippyContent = undefined

  export style = undefined
  export classes = undefined
  export id = undefined
  export disabled = false

  isShowing = false

  export events = {}

  


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
        tippyObject.hide()
        dispatch e.detail.event, e.detail.value
      return      

    onHide: (instance)->
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
  <button type="button" on:click use:popover={template} {disabled} {style} class={classes} {id}><slot/></button>
{/if}

<style lang="sass">


  button 
    display: inline-block
    padding: 0px
    background: none
    height: 24px
    min-width: 24px
    width: 24px
    border: none
    margin: 0px
    &:hover 
      background: none

</style>