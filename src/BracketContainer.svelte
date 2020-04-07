<script>
  import Bracket from "./Bracket.svelte";
  import TypeContainer from "./TypeContainer.svelte";
  import { afterUpdate } from "svelte";

  export let players;
  export let setWinner;

  let bracket = [];
  let remainingPlayers = players;
  let disabled = players.length < 3 ? true : false;
  let bracketType = "single";

  function clearBracket() {
    bracket = [];
    bracket = bracket;
  }

  function generateBracket() {
    let playerIndex = 0;
    let winnerCount = remainingPlayers.length;
    let length = Math.ceil(remainingPlayers.length / 2);
    let roundIndex = 1;
    while (Math.ceil(length) > 1) {
      bracket.push({
        round: roundIndex,
        gameCount:
          winnerCount / Math.ceil(length) === 2
            ? Math.ceil(length)
            : Math.ceil(length) - 1,
        byes: winnerCount / Math.ceil(length) === 2 ? false : true
      });
      length = Math.ceil(length / 2);
      winnerCount = Math.ceil(winnerCount / 2);
      roundIndex++;
    }
    bracket = bracket;
  }

  function setType(type) {
    bracketType = type;
    bracketType = bracketType;
  }

  afterUpdate(() => {
    disabled = players.length < 3 ? true : false;
  });
</script>

<style>
  button {
    padding: 0.25rem 0.5rem;
    transition-duration: 0.15s;
  }
</style>

<div class="flex flex-col items-center bg-white p-4 depth-shadow">
  <div class="flex flex-col w-full">
    <div class="w-full p-1">
      <TypeContainer {setType} {bracketType} />
    </div>
    <div class="flex flex-col w-full p-1 justify-center">
      <button
        class={disabled ? 'w-full bg-gray-300 text-gray-500 border-solid border-gray-300 border cursor-not-allowed hover:border-gray-500' : 'w-full depth-shadow bg-blue-500 text-white hover:bg-green-400'}
        {disabled}
        on:click={generateBracket}>
        Generate Turny
      </button>
    </div>
  </div>
  {#if bracket.length !== 0}
    <Bracket bind:bracket bind:remainingPlayers {setWinner} bind:bracketType />
  {:else}
    <p class="my-2 py-2 text-red-500 font-bold">
      You haven't generated a turny yet.
    </p>
  {/if}
</div>
