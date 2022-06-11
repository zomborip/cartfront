<template>
<div>
  <!-- [Screen] -->
  <div class="felx min-h-[100vh] bg-stone-200">
    <navbar />
    <!-- [Page] -->
    <div class="flex w-full bg-stone-200 flex-col pt-16">
      <!-- [Music Body] -->
      <div class="flex flex-col bg-stone-100 mt-12 ml-4 mr-4 align-top items-center p-1 rounded-lg lg:flex-row lg:items-start md:flex-row md:items-start sm:flex-row sm:items-start shadow-lg">
        <img :src="`/${apiData[0].img}.png`" class=" w-[20rem] z-0 rounded-[1rem]" >
        <div class="flex flex-col w-full px-5  justify-between lg:h-[20rem] lg:py-1 lg:flex-col-reverse md:h-[20rem] md:py-1 md:flex-col-reverse sm:h-[20rem] sm:py-1 sm:flex-col-reverse ">
          <div class="flex flex-row w-full justify-between">
            <div class="flex w-fit font-[Bahnschrift] text-lg lg:text-3xl md:text-3xl sm:text-3xl">{{apiData[0].name }}</div>
            <div class="flex w-fit text-lg font-light italic lg:text-3xl md:text-3xl sm:text-3xl">{{apiData[0].price}} $</div>
          </div>
          <div class="flex  flex-col">
            <div class="flex text-lg font-semibold w-fit border-b border-black mt-2 lg:text-3xl md:text-3xl sm:text-3xl">Description:</div>
            <div class="flex text-base mb-2 lg:text-lg">{{apiData[0].note}}</div>
          </div>
          </div>
      </div>
      <!-- [/Music Body] -->
      <div class="flex flex-row mt-1 ml-4 mr-4 justify-between mb-8npm">
        <div class="flex rounded-[0.5rem] bg-gray-400/40 p-2 cursor-pointer hover:scale-105 transition-all shadow-lg" @click="$router.push('/')">Back...</div>
        <div class="flex rounded-[0.5rem] bg-lime-200 p-2 cursor-pointer hover:scale-105 transition-all shadow-lg" @click="addCart()">Add To Cart</div>
      </div>
    </div>
    <!-- [/Page] -->
  </div>
  <!-- [/Screen] -->
  <!-- [Footerbar] -->
  <footerbar/>
  <!-- [/FooterBar] -->
</div>
</template>

<script setup>
  const route = useRoute()
  let song = {id: 1, name: "Song name #1", img: "default_logo", price: "10", note: "adasdasdsa"}
  let apiData = ref([{createdAt: "2022-06-11T13:07:48.000Z",demo: "asd",free: false,id: 1,img: "default_logo",name: "loading...",note: "loading...",note1: null,price: "0",prod: true,song: "asd"}])
  let result = await (await fetch(`http://localhost:3030/music/${route.params.id}`)).json()
  apiData = result
  const addCart = () => {
    //INIT STATE
    let st = useState('cart')
    if (typeof st.value == "undefined") { st.value = [] }
    
    //State add 
    if (!st.value.includes(apiData[0])) {st.value.push(apiData[0])}
    console.log(st.value);
  }
</script>

<style>

</style>