<script>
  export let final;
  export let setWinner;
</script>

<style>
  .player {
    position: relative;
    z-index: 1;
    padding: 50px;
    transition-duration: 0.15s;
  }
</style>

<div class="flex flex-col lg:flex-row justify-center items-center my-4">
  <div
    on:click={() => setWinner(final.players[0])}
    class="depth-shadow flex items-center justify-center player bg-blue-500
    text-white mx-2 hover:bg-green-400 w-full md:w-1/3 cursor-pointer">
    <h3 class="font-roboto-700 uppercase text-xl">{final.players[0]}</h3>
  </div>
  <i class="text-xl font-bold">vs.</i>
  <div
    on:click={() => setWinner(final.players[1])}
    class="depth-shadow flex items-center justify-center player bg-red-500
    text-white mx-2 hover:bg-green-400 w-full md:w-1/3 cursor-pointer">
    <h3 class="font-roboto-700 uppercase text-xl">{final.players[1]}</h3>
  </div>
</div>
