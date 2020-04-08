<script>
  import CloseCircle from "../node_modules/svelte-material-icons/CloseCircle.svelte";

  export let players;

  let currentValue = null;
  let invalidName = false;
  let height = "20px";
  let width = "20px";
  let disabled = true;

  const placeholders = [
    "Bill",
    "Kevin",
    "Tiger",
    "Arnold",
    "Jude",
    "David",
    "Jay",
    "Jack",
    "Jesse",
    "Woody"
  ];

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
    border: none;
  }

  input::placeholder {
    font-style: italic;
  }
</style>

<div class="bg-white p-4 depth-shadow">
  <h3 class="font-roboto-700 text-xl leading-tight">Add some participants!</h3>
  <i class="text-gray-400 text-xs mb-2">
    Enter each name of the people or teams participating.
  </i>
  <form on:submit={addPlayer} class="flex justify-center py-2 w-full">
    <div class="flex flex-row depth-shadow">
      <input
        class="py-1 px-2 bg-gray-200"
        name="player-input"
        type="text"
        maxlength="14"
        on:change={event => handleChange(event)}
        value={currentValue}
        placeholder={`ex: ${placeholders[Math.floor(Math.random() * Math.floor(placeholders.length - 1))]}`} />
      <span title="Add a participant">
        <button
          class="bg-blue-500 hover:bg-green-400 text-white cursor-pointer
          border-blue-500 hover:border-green-400 font-roboto-300"
          type="submit">
          Add
        </button>
      </span>

    </div>
  </form>
  <div>
    {#each players as player, i}
      <div
        id={i}
        class="flex flex-row justify-between bg-white my-2 py-1 px-4
        depth-shadow">
        <div>
          <span class="mr-2 text-green-500">{i + 1}</span>
          <b class="text-bold uppercase">{player}</b>
        </div>
        <span
          class="flex items-center cursor-pointer"
          on:click={() => removePlayer(i)}>
          <CloseCircle color="#f56565" {width} {height} />
        </span>
      </div>
    {/each}
  </div>
</div>
