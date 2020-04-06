<script>
  export let optionName;
  export let setType;
  export let bracketType;
  export let id;
</script>

<style>
  button {
    background-color: #63b3ed;
    color: #fff;
    width: 100%;
    height: 100%;
    transition-duration: 0.15s;
    padding: 13px;
  }

  .selected {
    background-color: #48bb78;
  }
</style>

<button
  class={id === bracketType ? 'selected depth-shadow' : 'depth-shadow'}
  on:click={() => setType(id)}>
  {optionName}
</button>
