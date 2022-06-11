<template>
  <div class="flex flex-row w-full h-16 py-3 bg-gradient-to-r from-red-400 via-orange-400 to-yellow-400 justify-between items-center fixed opacity-[0.85] z-10">
    <div class="flex font-bold text-lg items-center px-3 cursor-pointer " @click="$router.push({path: '/'})" >Kris Store</div>
    <div class="flex flex-row mx-3 group " @click="$router.push({path: '/cart'})">
      <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8 sm:hidden md:hidden lg:hidden" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
        <path stroke-linecap="round" stroke-linejoin="round" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
      </svg>
      <div class="bg-amber-500 rounded-md hidden sm:flex md:flex lg:flex py-2 px-4 text-lg cursor-pointer shadow-lg group-hover:scale-105 group-hover:transition-all">Shopping Cart</div>
      <div v-if="cNum > 0" class="flex h-min w-min bg-red-400 -ml-2 rounded-full group-hover:scale-105 group-hover:transition-all"> {{cNum}}</div>
    </div>
  </div>
</template>

<script setup>
  let cNum = ref(0)
  //INIT STATE
  let st = useState('cart')
  if (typeof st.value == "undefined") { st.value = [] }

  //Get Data From State
  console.log("NAV");
  console.log(st.value);
  cNum.value = st.value.length

  //watch
  watch(st.value, ()=> { cNum.value = st.value.length; console.log(`cNum Changed ${cNum.value}`); })


</script>
