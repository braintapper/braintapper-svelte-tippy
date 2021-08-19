<script>
  export let content = undefined;
</script>
<div>
  {@html content}
</div>
<style>
  div {
    padding: 8px;
    font-weight: bold;
    color: var(--white);
    background: var(--darkest-gray);
    border-radius: 4px;
  }
</style>