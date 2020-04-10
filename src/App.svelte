<script>
  import PlayerList from "./PlayerList.svelte";
  import Winner from "./Winner.svelte";
  import Tailwindcss from "./Tailwindcss.svelte";
  import BracketContainer from "./BracketContainer.svelte";
  import GithubCircle from "../node_modules/svelte-material-icons/GithubCircle.svelte";
  import { afterUpdate } from "svelte";

  let players = [];
  let winner = null;
  let bracketInitialized = false;

  function setWinner(finalWinner) {
    winner = finalWinner;
  }

  function initializeBracket() {
    bracketInitialized = true;
    bracketInitialized = bracketInitialized;
  }
</script>

<style>
  main {
    text-align: center;
    margin: 0 auto;
    min-height: 94vh;
  }

  h1 {
    font-weight: 800;
    line-height: 5rem;
  }
</style>

<main class="font-comfortaa">
  {#if winner}
    <Winner {winner} />
  {/if}
  <h1 class="font-700 font-comfortaa text-red-500 text-6xl">Turny</h1>
  <h2 class="mb-4">A simple tournament bracket manager</h2>
  <div class="flex flex-col xl:flex-row mx-2 md:mx-6 lg:mx-12">
    <div class="mb-4 px-4 w-full xl:w-1/3">
      <PlayerList bind:players {bracketInitialized} />
    </div>
    <div class="w-full xl:w-2/3">
      <BracketContainer
        bind:players
        {setWinner}
        {initializeBracket}
        {bracketInitialized} />
    </div>
  </div>
</main>
<div class="text-center my-4 bottom-0 right-0 left-0">
  <a
    href="https://github.com/ChaseMilligan/turny"
    target="_blank"
    class="flex flex-row items-center justify-center">
    <GithubCircle color="black" class="inline-block" />
    Turny on Github.
  </a>
</div>
