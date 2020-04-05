<script>
  import PlayerList from "./PlayerList.svelte";
  import Tailwindcss from "./Tailwindcss.svelte";
  import BracketContainer from "./BracketContainer.svelte";

  let players = [];
  let winner = null;

  function setWinner(finalWinner) {
    winner = finalWinner;
  }
</script>

<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    font-size: 4em;
    font-weight: 800;
  }

  .winner-mask {
    position: fixed;
    z-index: 10;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
  }

  .winner-mask h1 {
    font-size: 8rem;
    border-bottom: solid 1px #fff;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>

<main class="font-nunito">
  {#if winner}
    <div
      class="winner-mask flex flex-col items-center justify-center bg-green-500">
      <h2 class="uppercase text-white font-bold">Congratulations!</h2>
      <h1 class="uppercase text-white">{winner}</h1>
    </div>
  {/if}
  <h1 class="font-700 font-roboto text-red-400">Tourny</h1>
  <div class="flex flex-col md:flex-row mx-2 md:mx-6 lg:mx-12">
    <div class="px-1 w-full lg:w-1/3">
      <PlayerList bind:players />
    </div>
    <div class="px-1 w-full lg:w-2/3">
      <BracketContainer bind:players {setWinner} />
    </div>
  </div>
</main>
