<script>
  export let game;
  export let setGameWinner;
</script>

<style>
  .player {
    transition-duration: 0.15s;
    width: 50%;
  }

  .winner {
    background-color: #48bb78;
    width: 50%;
  }
</style>

<div class="px-2 w-full sm:w-1/2 lg:w-1/3 xl:w-1/4 text-white">
  <div class="my-2 bg-white depth-shadow">
    <h3
      class="font-roboto uppercase text-xl text-gray-400 border-solid
      border-gray-200 border border-b-0">
      {!game.gameWinner ? `Game ${game.game}` : 'Winner!'}
    </h3>
    <div class="flex flex-row">
      <div
        on:click={() => setGameWinner(game.game, game.players[0].name)}
        class={game.gameWinner === game.players[0].name ? 'winner player flex justify-center items-center bg-green-500 p-4' : 'player flex justify-center items-center bg-blue-500 hover:bg-green-400 p-4'}
        style={game.players.length === 1 ? 'width: 100%' : 'width: 50%'}>
        <p class="uppercase text-sm">{game.players[0].name}</p>
        {#if game.players.length === 1}
          <i class="ml-4">(BYE)</i>
        {/if}
      </div>
      {#if game.players.length >= 2}
        <div
          on:click={() => setGameWinner(game.game, game.players[1].name)}
          class={game.gameWinner === game.players[1].name ? 'winner flex justify-center items-center bg-green-500 p-4' : 'player flex justify-center items-center bg-red-500 hover:bg-green-400 p-4'}>
          <p class="uppercase text-sm">{game.players[1].name}</p>
        </div>
      {/if}
    </div>
  </div>
</div>
