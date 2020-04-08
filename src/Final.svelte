<script>
  import MenuUp from "../node_modules/svelte-material-icons/MenuUp.svelte";
  import MenuDown from "../node_modules/svelte-material-icons/MenuDown.svelte";
  import { afterUpdate } from "svelte";

  export let final;
  export let bracketType;
  export let score;
  export let handlePlayerScoreChange;
  export let setTempFinalWinner;

  afterUpdate(() => {
    if (bracketType !== "1") {
      if (
        score !== null &&
        final.gameWinner &&
        score[0] < Math.ceil(bracketType / 2) &&
        score[1] < Math.ceil(bracketType / 2)
      ) {
        setTempFinalWinner({ name: "" });
      }

      if (score !== null && score[0] > Math.ceil(bracketType / 2)) {
        handlePlayerScoreChange(final.game, 1, "down");
        if (score !== null && score[0] > Math.ceil(bracketType / 2)) {
          handlePlayerScoreChange(final.game, 1, "down");
        }
      }

      if (score !== null && score[1] > Math.ceil(bracketType / 2)) {
        handlePlayerScoreChange(final.game, 2, "down");
        if (score !== null && score[1] > Math.ceil(bracketType / 2)) {
          handlePlayerScoreChange(final.game, 2, "down");
        }
      }
    }
  });
</script>

<style>
  .player {
    position: relative;
    z-index: 1;
    padding: 50px;
    transition-duration: 0.15s;
  }

  .winner {
    background-color: #48bb78;
  }

  .counter-arrow {
    height: 50%;
  }

  .counter-arrow:hover {
    background-color: rgba(0, 0, 0, 0.25);
  }
</style>

<div class="flex flex-col lg:flex-row justify-center items-center my-4">
  {#if bracketType === '1'}
    <div
      on:click={() => setTempFinalWinner(final.players[0])}
      class={final.gameWinner === final.players[0].name ? 'winner depth-shadow flex items-center justify-center player text-white mx-2 hover:bg-green-400 w-full md:w-1/3 cursor-pointer' : 'depth-shadow flex items-center justify-center player bg-blue-500 text-white mx-2 hover:bg-green-400 w-full md:w-1/3 cursor-pointer'}>
      <h3 class="font-roboto-700 uppercase text-xl">{final.players[0].name}</h3>
    </div>
    <i class="text-xl font-bold">vs.</i>
    <div
      on:click={() => setTempFinalWinner(final.players[1])}
      class={final.gameWinner === final.players[1].name ? 'winner depth-shadow flex items-center justify-center player text-white mx-2 hover:bg-green-400 w-full md:w-1/3 cursor-pointer' : 'depth-shadow flex items-center justify-center player bg-red-500 text-white mx-2 hover:bg-green-400 w-full md:w-1/3 cursor-pointer'}>
      <h3 class="font-roboto-700 uppercase text-xl">{final.players[1].name}</h3>
    </div>
  {:else}
    <div class="flex flex-col w-full md:w-1/3 mx-2">
      <div class="flex flex-row justify-around bg-gray-300 py-1 px-2">
        {final.players[0].name}
      </div>
      <div
        class={final.gameWinner === final.players[0].name ? 'winner depth-shadow flex items-center justify-center player text-white w-full cursor-pointer' : 'depth-shadow flex items-center justify-center player bg-blue-500 text-white w-full cursor-pointer'}>
        <span
          class="flex flex-col items-center justify-center cursor-pointer w-full
          counter-arrow absolute top-0 pb-2"
          on:click={() => handlePlayerScoreChange(final.game, 1, 'up')}>
          <MenuUp />
        </span>
        <h3 class="font-roboto-700 uppercase text-xl">{score[0]}</h3>
        <span
          class="flex flex-col items-center justify-center cursor-pointer w-full
          counter-arrow absolute bottom-0 pt-2"
          on:click={() => handlePlayerScoreChange(final.game, 1, 'down')}>
          <MenuDown />
        </span>
      </div>
    </div>
    <i class="text-xl font-bold">vs.</i>
    <div class="flex flex-col w-full md:w-1/3 mx-2">
      <div class="flex flex-row justify-around bg-gray-300 py-1 px-2">
        {final.players[1].name}
      </div>
      <div
        class={final.gameWinner === final.players[1].name ? 'winner depth-shadow flex items-center justify-center player text-white w-full cursor-pointer' : 'depth-shadow flex items-center justify-center player bg-red-500 text-white w-full cursor-pointer'}>
        <span
          class="flex flex-col items-center justify-center cursor-pointer w-full
          counter-arrow absolute top-0 pb-2"
          on:click={() => handlePlayerScoreChange(final.game, 2, 'up')}>
          <MenuUp />
        </span>
        <h3 class="font-roboto-700 uppercase text-xl">{score[1]}</h3>
        <span
          class="flex flex-col items-center justify-center cursor-pointer w-full
          counter-arrow absolute bottom-0 pt-2"
          on:click={() => handlePlayerScoreChange(final.game, 2, 'down')}>
          <MenuDown />
        </span>
      </div>
    </div>
  {/if}
</div>
