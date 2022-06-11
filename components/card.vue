<template>
  <div class="flex flex-col items-center justify-center mb-7 md:w-[20rem] md:h-[20rem] lg:w-[20rem] lg:h-[20rem] cursor-pointer hover:scale-105 hover:shadow-lg hover:transition-all  hover:rounded-2xl" @click="$router.push('/music/1')">
    <img :src="`/${cardImg}.png`" class="flex h-[80%] w-[80%] sm:w-[80%] md:w-[80%] md:h-[80%] lg:w-[80%] lg:h-[80%] rounded-2xl ">
    <div class="flex flex-row justify-between w-[75%] ">
      <div class="flex font-[Bahnschrift] text-lg font-medium">{{cardLabel}}</div>
      <div class="flex font-[Bahnschrift] text-lg font-thin">{{cardPrice}} $</div>
    </div>
  </div>
</template>

<script setup>
  const props = defineProps(["cardLabel", "cardImg", "cardId", "cardPrice"])
</script>

<style>

</style>