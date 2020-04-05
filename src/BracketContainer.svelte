<script>
  import BracketGenerator from "../node_modules/bracket-generator";
  import Bracket from "./Bracket.svelte";
  import { afterUpdate } from "svelte";

  export let players;
  export let setWinner;

  let bracket = [];
  let remainingPlayers = players;

  function clearBracket() {
    bracket = [];
    bracket = bracket;
  }

  function generateBracket() {
    let playerIndex = 0;
    let length = players.length / 2;
    let roundIndex = 1;
    while (Math.ceil(length) > 1) {
      bracket.push({
        round: roundIndex,
        gameCount:
          Math.ceil(length) % 2 === 0
            ? Math.ceil(length)
            : Math.ceil(length) - 1,
        byes: Math.ceil(length) % 2
      });
      length = Math.ceil(length) / 2;
      roundIndex++;
    }
    bracket = bracket;
  }
</script>

<style>
  button {
    padding: 0.25rem 0.5rem;
    transition-duration: 0.15s;
    border-radius: 5px;
  }
</style>

<div class="bg-white p-4 border-solid border-gray-700 border-2">
  <h3 class="font-roboto-700 uppercase text-xl">Tourny</h3>
  <button
    disabled={players.length < 3 ? true : false}
    on:click={generateBracket}>
    Generate Tourny
  </button>
  <button disabled={bracket.length === 0} on:click={clearBracket}>
    Clear Tourny
  </button>
  {#if bracket.length !== 0}
    <Bracket bind:bracket bind:remainingPlayers {setWinner} />
  {:else}
    <p class="my-2 py-2 text-red-400 font-bold">
      You haven't generated a tourny yet.
    </p>
  {/if}
</div>
