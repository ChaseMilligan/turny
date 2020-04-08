<script>
  import MenuUp from "../node_modules/svelte-material-icons/MenuUp.svelte";
  import MenuDown from "../node_modules/svelte-material-icons/MenuDown.svelte";
  import { onMount, afterUpdate } from "svelte";

  export let game;
  export let setGameWinner;
  export let bracketType;
  export let score;
  export let handlePlayerScoreChange;

  let width = "70px";
  let height = "70px";

  afterUpdate(() => {
    if (bracketType !== "1") {
      if (
        score !== null &&
        game.gameWinner &&
        score[0] < Math.ceil(bracketType / 2) &&
        score[1] < Math.ceil(bracketType / 2)
      ) {
        setGameWinner(game.game, "");
      }

      if (score !== null && score[0] > Math.ceil(bracketType / 2)) {
        handlePlayerScoreChange(game.game, 1, "down");
        if (score !== null && score[0] > Math.ceil(bracketType / 2)) {
          handlePlayerScoreChange(game.game, 1, "down");
        }
      }

      if (score !== null && score[1] > Math.ceil(bracketType / 2)) {
        handlePlayerScoreChange(game.game, 2, "down");
        if (score !== null && score[1] > Math.ceil(bracketType / 2)) {
          handlePlayerScoreChange(game.game, 2, "down");
        }
      }
    }
  });
</script>

<style>
  .player {
    transition-duration: 0.15s;
    width: 50%;
    position: relative;
  }

  .winner {
    background-color: #48bb78;
    width: 50%;
  }

  .counter-arrow {
    height: 50%;
  }

  .counter-arrow:hover {
    background-color: rgba(0, 0, 0, 0.25);
  }
</style>

<div class="self-stretch px-2 w-full sm:w-1/2 lg:w-1/3 xl:w-1/4 text-white">
  <div class="h-full flex flex-col my-2 bg-white depth-shadow">
    <h3
      class="font-roboto uppercase text-xl text-gray-400 border-solid
      border-gray-200 border border-b-0">
      {!game.gameWinner ? `Game ${game.game}` : 'Winner!'}
    </h3>
    <div class="flex flex-col h-full">
      {#if bracketType !== '1' && game.players.length !== 1}
        <div class="flex flex-row justify-around bg-gray-300 py-1 px-2">
          <span class="text-gray-600">{game.players[0].name}</span>
          <span class="text-gray-600">{game.players[1].name}</span>
        </div>
      {/if}
      <div class="flex flex-row h-full">
        {#if bracketType === '1'}
          <div
            on:click={() => setGameWinner(game.game, game.players[0].name)}
            class={game.gameWinner === game.players[0].name ? 'winner player flex justify-center items-center bg-green-500 p-4' : 'player flex justify-center items-center bg-blue-500 hover:bg-green-400 p-4'}
            style={game.players.length === 1 ? 'width: 100%' : 'width: 50%'}>
            <p class="uppercase text-sm">{game.players[0].name}</p>
            {#if game.players.length === 1}
              <i class="ml-4 text-sm">(BYE)</i>
            {/if}
          </div>
          {#if game.players.length >= 2}
            <div
              on:click={() => setGameWinner(game.game, game.players[1].name)}
              class={game.gameWinner === game.players[1].name ? 'winner flex flex-col justify-center items-center bg-green-500 p-4' : 'player flex flex-col justify-center items-center bg-red-500 hover:bg-green-400 p-4'}>
              <p class="uppercase text-sm m-0">{game.players[1].name}</p>
            </div>
          {/if}
        {:else}
          <div
            class={game.gameWinner === game.players[0].name ? 'winner player flex justify-center items-center bg-green-500 p-4' : 'player flex justify-center items-center bg-blue-500 p-4'}
            style={game.players.length === 1 ? 'width: 100%' : 'width: 50%'}>

            {#if game.players.length === 1}
              <p class="uppercase text-sm">{game.players[0].name}</p>
              <i class="ml-4 text-sm">(BYE)</i>
            {:else}
              <span
                class="flex flex-col items-center justify-center cursor-pointer
                w-full counter-arrow absolute top-0 pb-2"
                on:click={() => handlePlayerScoreChange(game.game, 1, 'up')}>
                <MenuUp />
              </span>
              <p class="uppercase text-2xl m-0">{score[0]}</p>
              <span
                class="flex flex-col items-center justify-center cursor-pointer
                w-full counter-arrow absolute bottom-0 pt-2"
                on:click={() => handlePlayerScoreChange(game.game, 1, 'down')}>
                <MenuDown />
              </span>
            {/if}
          </div>
          {#if game.players.length >= 2}
            <div
              class={game.gameWinner === game.players[1].name ? 'winner player flex justify-center items-center bg-green-500 p-4' : 'player flex justify-center items-center bg-red-500 p-4'}>
              <span
                class="flex flex-col items-center justify-center cursor-pointer
                w-full counter-arrow absolute top-0 pb-2"
                on:click={() => handlePlayerScoreChange(game.game, 2, 'up')}>
                <MenuUp />
              </span>
              <p class="uppercase text-2xl m-0">{score[1]}</p>
              <span
                class="flex flex-col items-center justify-center cursor-pointer
                w-full counter-arrow absolute bottom-0 pt-2"
                on:click={() => handlePlayerScoreChange(game.game, 2, 'down')}>
                <MenuDown />
              </span>
            </div>
          {/if}
        {/if}
      </div>
    </div>
  </div>
</div>
