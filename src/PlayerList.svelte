<script>
  import CloseCircle from "../node_modules/svelte-material-icons/CloseCircle.svelte";

  export let players;

  let currentValue = null;
  let invalidName = false;
  let height = "20px";
  let width = "20px";
  let disabled = true;

  function handleChange(event) {
    currentValue = event.target.value;
  }

  function removePlayer(id) {
    if (id > -1) {
      players.splice(id, 1);
    }
    players = players;
  }

  function addPlayer() {
    event.preventDefault();
    if (!currentValue) {
      return;
    }
    players.push(currentValue);
    players = players;
    currentValue = null;
  }
</script>

<style>
  button {
    padding: 0.25rem 0.5rem;
    transition-duration: 0.15s;
  }

  input {
    border-right: none;
    border-radius: 5px 0px 0px 5px;
  }

  .add-btn {
    border-radius: 0px 5px 5px 0px;
  }
</style>

<div class="bg-white p-4 border-solid border-gray-700 border-2">
  <h3 class="font-roboto-700 uppercase text-xl">Player List</h3>
  <form on:submit={addPlayer} class="flex justify-center pb-2 w-full">
    <div class="flex flex-row">
      <input
        class="py-1 px-2"
        name="player-input"
        type="text"
        maxlength="14"
        on:change={event => handleChange(event)}
        value={currentValue}
        placeholder="Enter player name" />
      <button
        class="add-btn text-gray-700 bg-white hover:bg-blue-500 hover:text-white
        cursor-pointer border-blue-500 font-roboto-300"
        type="submit">
        Add
      </button>
    </div>
  </form>
  <div>
    {#each players as player, i}
      <div
        id={i}
        class="flex flex-row justify-between py-1 px-4 border-solid
        border-gray-500 border-b">
        <div>
          <span class="mr-2">{i + 1}</span>
          <b class="text-bold uppercase" {disabled}>{player}</b>
        </div>
        <span
          class="flex items-center cursor-pointer"
          on:click={() => removePlayer(i)}>
          <CloseCircle color="#fc8181" {width} {height} />
        </span>
      </div>
    {/each}
  </div>
</div>
