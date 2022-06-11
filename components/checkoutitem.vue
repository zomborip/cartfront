<template>
  <div class="flex flex-col lg:flex-row md:flex-row w-full shadow-sm mt-2">
    <div class="flex flex-row w-[100%] ">
      <img :src="`/${songImg}.png`" class="flex h-[5rem] lg:h-[10rem] md:h-[10rem] self-baseline ">
    </div>
    <div class="flex flex-row w-full justify-between">
      <div class="flex text-base lg:items-end md:items-end lg:text-xl md:text-xl ">{{songName}}</div>
      <div class="flex text-thin italic lg:items-end md:items-end lg:text-xl md:text-xl "> {{songPrice}} $ </div>
    </div>
  </div>
</template>

<script setup>
 const props = defineProps(["songName", "songImg", "songId", "songPrice"])
</script>

<style>

</style>