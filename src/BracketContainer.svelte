<script>
  import Bracket from "./Bracket.svelte";
  import TypeButton from "./TypeButton.svelte";
  import { afterUpdate } from "svelte";

  export let players;
  export let setWinner;

  let bracket = [];
  let remainingPlayers = players;
  let disabled = players.length < 3 ? true : false;

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
      console.log(length);
      console.log(winnerCount);
      console.log(winnerCount / Math.ceil(length));
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
  <div class="flex flex-col md:flex-row">
    <h3 class="font-roboto-700 text-xl">Turny Type</h3>
    <div
      class="flex flex-row flex-wrap p-2 bg-gray-200 depth-shadow mb-2 w-full">
      <div class="flex items-center justify-center w-full md:w-1/2 p-1">
        <TypeButton optionName={'Single Elimination'} />
      </div>
      <div class="flex items-center justify-center w-full md:w-1/2 p-1">
        <TypeButton optionName={'Best of 3'} />
      </div>
      <div class="flex items-center justify-center w-full md:w-1/2 p-1">
        <TypeButton optionName={'Best of 5'} />
      </div>
      <div class="flex items-center justify-center w-full md:w-1/2 p-1">
        <TypeButton optionName={'Best of 7'} />
      </div>
    </div>
    <button
      class={disabled ? 'w-full bg-gray-300 text-gray-500 border-solid border-gray-300 border cursor-not-allowed hover:border-gray-500' : 'w-full depth-shadow bg-blue-500 text-white hover:bg-green-400'}
      {disabled}
      on:click={generateBracket}>
      Generate Turny
    </button>
  </div>
  {#if bracket.length !== 0}
    <Bracket bind:bracket bind:remainingPlayers {setWinner} />
  {:else}
    <p class="my-2 py-2 text-red-500 font-bold">
      You haven't generated a turny yet.
    </p>
  {/if}
</div>
