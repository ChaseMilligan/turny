<script>
  export let winner;
</script>

<style>
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

<div class="winner-mask flex flex-col items-center justify-center bg-green-500">
  <h2 class="uppercase font-comfortaa text-white font-bold">
    Congratulations!
  </h2>
  <h1 class="uppercase text-white text-6xl sm:text-8xl">{winner}</h1>
</div>
