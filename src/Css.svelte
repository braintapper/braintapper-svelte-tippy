<style>
:global(:root) {
  --tooltip-background: var(--black);
  --tooltip-foreground: var(--foreground-dark); }
  @media (prefers-color-scheme: dark) {
    :global(:root) {
      --tooltip-background: var(--dark-gray);
      --tooltip-foreground: var(--foreground-dark); } }

:global(.tippy-box[data-animation=fade][data-state=hidden]) {
  opacity: 0; }

:global([data-tippy-root]) {
  max-width: calc(100vw - 10px); }

:globla(.tippy-box) {
  position: relative;
  background-color: var(--tooltip-background);
  color: var(--tooltip-foreground);
  border-radius: 4px;
  font-size: 12px;
  line-height: 1.4;
  outline: 0;
  transition-property: transform,visibility,opacity; }

  :global(.tippy-box[data-placement^=top] > .tippy-arrow) {
    bottom: 0; }

  :global(.tippy-box:before) {
    bottom: -7px;
    left: 0;
    border-width: 8px 8px 0;
    border-top-color: initial;
    transform-origin: center top; }

  :global(.tippy-box[data-placement^=bottom] > .tippy-arrow) {
    top: 0; }

  :global(.tippy-box:before) {
    top: -7px;
    left: 0;
    border-width: 0 8px 8px;
    border-bottom-color: initial;
    transform-origin: center bottom; }

  :global(.tippy-box[data-placement^=left] > .tippy-arrow) {
    right: 0; }

  :global(.tippy-box:before) {
    border-width: 8px 0 8px 8px;
    border-left-color: initial;
    right: -7px;
    transform-origin: center left; }

  :global(.tippy-box[data-placement^=right] > .tippy-arrow) {
    left: 0; }

  :global(.tippy-box:before) {
    left: -7px;
    border-width: 8px 8px 8px 0;
    border-right-color: initial;
    transform-origin: center right; }

  :global(.tippy-box[data-inertia][data-state=visible]) {
    transition-timing-function: cubic-bezier(0.54, 1.5, 0.38, 1.11); }

:global(.tippy-arrow) {
  width: 16px;
  height: 16px;
  color: var(--tooltip-background); }

  :global(.tippy-arrow:before) {
    content: "";
    position: absolute;
    border-color: transparent;
    border-style: solid; }

:global(.tippy-content) {
  position: relative;
  padding: 5px 9px;
  z-index: 1; }

:global(.tippy-box) {
  background-color: var(--white);
  border-radius: 0;
  box-shadow: rgba(60, 64, 67, 0.3) 0px 1px 2px 0px, rgba(60, 64, 67, 0.15) 0px 1px 3px 1px;
  color: var(--black); }

  :global(.tippy-box[data-theme="datepicker"]) {
    width: 280px; }

  :global(.tippy-box[data-theme="menu"]) {
    width: 240px; }

  :global(.tippy-box[data-theme="menu"] .tippy-content) {
    padding: 0px; }

  :global(.tippy-box[data-theme="menu"] ul[role="menu"] hr) {
    border: none;
    border-bottom: 1px solid var(--lightest-gray); }

  :global(.tippy-box[data-theme="menu"] ul[role="menu"] li button) {
    min-height: 32px; }

:global(.tippy-box[data-theme="menu"]) {
  background-color: var(--white);
  border-radius: 0;
  width: 240px; }

:global(.tippy-box[data-theme="context-menu"]) {
  background-color: var(--white);
  border-radius: 0;
  width: 240px; }

:global(.tippy-box .tippy-content) {
  padding: 0px; }

</style>