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
    margin: 0 auto;
  }

  h1 {
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
    border-bottom: solid 1px #fff;
  }
</style>

<main class="font-comfortaa">
  {#if winner}
    <div
      class="winner-mask flex flex-col items-center justify-center bg-green-500">
      <h2 class="uppercase font-comfortaa text-white font-bold">
        Congratulations!
      </h2>
      <h1 class="uppercase text-white text-6xl sm:text-8xl">{winner}</h1>
    </div>
  {/if}
  <h1 class="font-700 font-comfortaa text-red-500 text-6xl">Turny</h1>
  <div class="flex flex-col-reverse xl:flex-row mx-2 md:mx-6 lg:mx-12">
    <div class="mb-4 px-1 w-full xl:w-1/3">
      <PlayerList bind:players />
    </div>
    <div class="px-1 w-full xl:w-2/3">
      <BracketContainer bind:players {setWinner} />
    </div>
  </div>
</main>
