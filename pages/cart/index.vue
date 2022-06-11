<template>
<div>
  <!-- [Screen] -->
  <div class="felx min-h-[100vh] bg-stone-200">
    <navbar />

      <!-- [Body] -->
      <div class="flex flex-col h-full w-full pt-16 items-center ">
        <!-- [Cart] -->
        <div class="flex flex-col h-full w-[90%] lg:w-[70%] md:w-[70%] sm:w-[90%]  mt-6 bg-stone-100 shadow-xl rounded-lg p-1 ">
          <div class="flex flex-row text-3xl pl-2 font-medium">Shopping Cart</div>
          <div class="flex flex-col w-full pt-3 pl-2">
            <!-- [Checkout Items] -->
            <checkoutitem v-for="i in st" :songName="i.name" :songImg="i.img" :songPrice="i.price" :songId="i.id" />
            <!-- [/Checkout Items] -->
            <!-- [Total] -->
            <div class="flex flex-row h-full w-full justify-between">
              <div class="flex font-semibold text-lg">Total:</div>
              <div class="flex font-semibold text-lg italic">{{p}} $</div>
            </div>
            <!-- [/Total] -->
          </div>
        </div>
        <!-- [/Cart] -->
        <div class="flex flex-row w-[90%] lg:w-[70%] md:w-[70%] sm:w-[90%] items-end justify-between px-1">
          <div class="flex rounded-[0.5rem] bg-gray-300 p-2 mt-2 cursor-pointer hover:scale-105 transition-all shadow-xl" @click="$router.back()">Back...</div>
          <div class="flex rounded-[0.5rem] bg-teal-200 p-2 mt-2 cursor-pointer hover:scale-105 transition-all shadow-xl" @click="pay()">Checkout</div>
        </div>
      </div>
      <!-- [/Body] -->

  </div>
  <!-- [/Screen] -->
  <footerbar />
</div>
</template>

<script setup>
  const vals = ref([
    {cid: 1, cl: "Song name #1", sp: "default_logo", p: "10"},
    {cid: 2, cl: "Cool Music Label", sp: "default_logo", p: "2"},
    {cid: 3, cl: "Some Audio", sp: "default_logo", p: "4"},
  ])
  //INIT STATE
  let st = useState('cart')
  if (typeof st.value == "undefined") { st.value = [] }

  //calculate price
  let p = ref(0)
  for (let i in st.value) { p.value = parseInt(st.value[i].price) + parseInt(p.value) }

  //checkout
  let pay = () => {
    st.value = []
  }
</script>

<style>

</style>