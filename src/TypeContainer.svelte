<script>
  import TypeButton from "./TypeButton.svelte";

  export let setType;
  export let bracketType;
</script>

<h3 class="font-roboto-700 text-xl leading-tight">Pick a Turny Style</h3>
<i class="text-gray-400 text-xs mb-2">
  The type you choose can be changed after you generate a Turny.
</i>
<div class="flex flex-row flex-wrap p-2 bg-gray-200 depth-shadow my-4 w-full">
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
