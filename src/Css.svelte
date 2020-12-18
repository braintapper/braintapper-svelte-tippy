<style global lang="sass">
  ///* tippy */

  // note: add theme items to global (here)


  
  \:root

    --tooltip-background: var(--black)
    --tooltip-foreground: var(--foreground-dark)

    @media (prefers-color-scheme: dark)
      --tooltip-background: var(--dark-gray)
      --tooltip-foreground: var(--foreground-dark)

  .tippy-box[data-animation=fade][data-state=hidden]
    opacity: 0

  [data-tippy-root]
    max-width: calc(100vw - 10px)

  .tippy-box
    position: relative
    background-color: var(--tooltip-background)
    color: var(--tooltip-foreground)
    border-radius: 4px
    font-size: 12px
    line-height: 1.4
    outline: 0
    transition-property: transform,visibility,opacity



    &[data-placement^=top]>.tippy-arrow
      bottom: 0
      
    &:before
      bottom: -7px
      left: 0
      border-width: 8px 8px 0
      border-top-color: initial
      transform-origin: center top


    &[data-placement^=bottom]>.tippy-arrow
      top: 0
    &:before
      top: -7px
      left: 0
      border-width: 0 8px 8px
      border-bottom-color: initial
      transform-origin: center bottom


    &[data-placement^=left]>.tippy-arrow
      right: 0
    &:before
      border-width: 8px 0 8px 8px
      border-left-color: initial
      right: -7px
      transform-origin: center left


    &[data-placement^=right]>.tippy-arrow
      left: 0
    &:before
      left: -7px
      border-width: 8px 8px 8px 0
      border-right-color: initial
      transform-origin: center right


    &[data-inertia][data-state=visible]
      transition-timing-function: cubic-bezier(.54,1.5,.38,1.11)


  .tippy-arrow
    width: 16px
    height: 16px
    color: var(--tooltip-background)
    &:before
      content: ""
      position: absolute
      border-color: transparent
      border-style: solid


  .tippy-content
    position: relative
    padding: 5px 9px
    z-index: 1


  .tippy-box
    background-color: var(--white)
    // border: 1px solid var(--gray)
    border-radius: 0

    //box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px
    box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 1px 3px 1px

    color: var(--black)

    &[data-theme="datepicker"]
      width: 280px
      

    &[data-theme="menu"]
      width: 240px
    &[data-theme="menu"]
      .tippy-content
        padding: 0px
      ul[role="menu"]
        hr
          border: none
          border-bottom: 1px solid var(--lightest-gray)
        li
          button
            min-height: 32px

  .tippy-box
    &[data-theme="menu"]
      background-color: var(--white)
      
      border-radius: 0
      width: 240px


  .tippy-box
    &[data-theme="context-menu"]
      background-color: var(--white)
      border-radius: 0
      width: 240px
    .tippy-content
      padding: 0px      
</style>