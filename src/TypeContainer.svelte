<script>
  import TypeButton from "./TypeButton.svelte";

  export let setType;
  export let bracketType;
</script>

<h3 class="font-roboto-700 text-xl mb-2">Turny Style</h3>
<div class="flex flex-row flex-wrap p-2 bg-gray-200 depth-shadow mb-4 w-full">
  <div class="flex items-center justify-center w-full md:w-1/2 lg:w-1/4 p-1">
    <TypeButton
      optionName={'Single Elimination'}
      id={'1'}
      {setType}
      {bracketType} />
  </div>
  <div class="flex items-center justify-center w-full md:w-1/2 lg:w-1/4 p-1">
    <TypeButton optionName={'Best of 3'} id={'3'} {setType} {bracketType} />
  </div>
  <div class="flex items-center justify-center w-full md:w-1/2 lg:w-1/4 p-1">
    <TypeButton optionName={'Best of 5'} id={'5'} {setType} {bracketType} />
  </div>
  <div class="flex items-center justify-center w-full md:w-1/2 lg:w-1/4 p-1">
    <TypeButton optionName={'Best of 7'} id={'7'} {setType} {bracketType} />
  </div>
</div>
