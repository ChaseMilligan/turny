<script>
  import Game from "./Game.svelte";
  import Final from "./Final.svelte";
  import { onMount, afterUpdate } from "svelte";

  export let bracket;
  export let remainingPlayers;
  export let setWinner;

  let allGames = [];
  let final = null;
  let currentRound = 1;

  function populateBracket() {
    let playerIndex = 0;
    for (let i = 0; i < Math.ceil(remainingPlayers.length / 2); i++) {
      if (i === 0 && !!bracket[currentRound - 1].byes) {
        allGames.push({
          game: 1,
          players: [
            {
              name: remainingPlayers[playerIndex],
              bye: bracket[currentRound - 1].byes !== 0 ? true : false
            }
          ],
          gameWinner: remainingPlayers[playerIndex]
        });
        playerIndex += 1;
      } else {
        if (!remainingPlayers[playerIndex + 1]) {
          allGames.push({
            game: i + 1,
            players: [
              {
                name: remainingPlayers[playerIndex],
                bye: true
              }
            ],
            gameWinner: remainingPlayers[playerIndex]
          });
        } else {
          allGames.push({
            game: i + 1,
            players: [
              {
                name: remainingPlayers[playerIndex],
                bye: false
              },
              {
                name: remainingPlayers[playerIndex + 1],
                bye: false
              }
            ],
            gameWinner: null
          });
        }
        playerIndex += 2;
      }
    }
    allGames = allGames;
  }

  function setGameWinner(gameId, playerName) {
    allGames[gameId - 1].gameWinner = playerName;
    allGames = allGames;
  }

  function nextRound() {
    currentRound += 1;
    remainingPlayers = [];
    for (let i = 0; i < allGames.length; i++) {
      remainingPlayers.push(allGames[i].gameWinner);
    }
    allGames = [];
    remainingPlayers = remainingPlayers;
    if (currentRound > bracket.length) {
      setupFinal();
      return;
    }
    populateBracket();
  }

  function setupFinal() {
    final = {
      players: remainingPlayers,
      gameWinner: null
    };
    final = final;
  }

  onMount(() => {
    console.log(bracket);
    populateBracket();
  });

  afterUpdate(() => {
    console.log(allGames);
  });
</script>

<style>
  button {
    padding: 0.25rem 0.5rem;
    transition-duration: 0.15s;
    border-radius: 5px;
  }
</style>

<div class="my-2 py-2">
  <h3 class="font-roboto-700 uppercase text-xl">
    {currentRound > bracket.length ? 'Final' : `Round ${currentRound}`}
  </h3>
  {#if !final}
    <div class="flex flex-col lg:flex-row flex-wrap justify-center my-4">
      {#each allGames as game, i}
        <Game {game} {setGameWinner} />
      {/each}
    </div>
  {:else}
    <Final {final} {setWinner} />
  {/if}
  <button
    on:click={nextRound}
    disabled={!!allGames.find(game => game.gameWinner === null)}>
    Next Round
  </button>
</div>
