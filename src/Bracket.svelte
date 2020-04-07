<script>
  import Game from "./Game.svelte";
  import Final from "./Final.svelte";
  import { onMount, afterUpdate } from "svelte";

  export let bracket;
  export let remainingPlayers;
  export let setWinner;
  export let bracketType;

  let allGames = [];
  let final = null;
  let currentRound = 1;
  let disabled = !!allGames.find(game => game.gameWinner === null);

  function populateBracket() {
    let playerIndex = 0;
    allGames = [];
    remainingPlayers = shuffle(remainingPlayers);
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
          score: null,
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
            score: null,
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
            score: [0, 0],
            gameWinner: null
          });
        }
        playerIndex += 2;
      }
    }
    allGames = allGames;
  }

  function completeGame(gameId) {
    completeGames.push(gameId);
    completeGames = completeGames;
  }

  function shuffle(array) {
    // https://stackoverflow.com/questions/2450954/how-to-randomize-shuffle-a-javascript-array
    var currentIndex = array.length,
      temporaryValue,
      randomIndex;

    // While there remain elements to shuffle...
    while (0 !== currentIndex) {
      // Pick a remaining element...
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex -= 1;

      // And swap it with the current element.
      temporaryValue = array[currentIndex];
      array[currentIndex] = array[randomIndex];
      array[randomIndex] = temporaryValue;
    }

    return array;
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
      allGames[i].gameWinner = "";
    }
    remainingPlayers = shuffle(remainingPlayers);
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

  function handlePlayerScoreChange(gameNumber, player, direction) {
    const gameId = gameNumber - 1;
    const playerId = player - 1;
    const game = allGames[gameId];

    if (player === 1 && game.gameWinner === game.players[1].name) {
      return;
    }
    if (player === 2 && game.gameWinner === game.players[0].name) {
      return;
    }

    if (direction === "up") {
      if (
        game.score[playerId] === Math.ceil(bracketType / 2) ||
        game.gameWinner === game.players[playerId].name
      ) {
        return;
      }
      game.score[playerId] += 1;
      allGames = allGames;
      if (game.score[playerId] >= Math.ceil(bracketType / 2)) {
        setGameWinner(game.game, game.players[playerId].name);
        return;
      }
      return;
    }
    if (direction === "down") {
      if (game.score[playerId] === 0) {
        return;
      }
      game.score[playerId] -= 1;
      allGames = allGames;
      if (game.score[playerId] < Math.ceil(bracketType / 2)) {
        setGameWinner(game.game, "");
      }
      return;
    }
  }

  onMount(() => {
    remainingPlayers = shuffle(remainingPlayers);
    populateBracket();
  });

  afterUpdate(() => {
    disabled = !!allGames.find(game => game.gameWinner === null);
  });
</script>

<style>
  button {
    padding: 0.25rem 0.5rem;
    transition-duration: 0.15s;
  }
</style>

<div class="w-full my-2 py-2">
  <h3 class="font-roboto-700 uppercase text-xl">
    {currentRound > bracket.length ? 'Final' : `Round ${currentRound}`}
  </h3>
  {#if !final}
    {#if allGames !== []}
      <div class="flex flex-col lg:flex-row flex-wrap justify-center my-8">
        {#each allGames as game, i}
          <Game
            bind:game
            {setGameWinner}
            bind:bracketType
            score={game.score}
            {handlePlayerScoreChange} />
        {/each}
      </div>
    {/if}
  {:else}
    <Final {final} {setWinner} />
  {/if}
  <button
    class={disabled ? 'bg-gray-300 text-gray-700 border-solid border-gray-300 border cursor-not-allowed hover:border-gray-500' : 'depth-shadow bg-blue-500 text-white hover:bg-green-400'}
    on:click={nextRound}
    {disabled}>
    Next Round
  </button>
</div>
