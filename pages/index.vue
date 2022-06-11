<template>
<div>
  <!-- [Screen] -->
  <div class="felx min-h-[100vh] bg-stone-200 ">
    <navbar></navbar>
    <!-- [Body]  -->
    <div class="flex bg-stone-200 w-full flex-col pt-16 ">
      <!-- [MidField] -->      
      <div class="flex flex-col bg-stone-100 w-auto h-auto m-5 mt-7 p-3 rounded-xl shadow-lg">
        <!-- [Search Sort] -->
        <div class="flex flex-row w-auto py-1 justify-between " >
          <input type="text" v-model="searchTxt" @input="a" placeholder="Search..." class="flex w-[6rem] sm:w-auto md:w-auto lg:w-auto h-min p-1 rounded-lg placeholder:italic text-lime-600 ">
          <select id="sort-select" v-model="sortMode" @change="a" class="flex rounded-lg pl-3 ">
              <option value="default">Sort By...</option>
              <optgroup label="Price">
                  <option value="pAsc">Cheap</option>
                  <option value="pDesc">Expensive</option>
              </optgroup>
              <optgroup label="Name">
                  <option value="nAsc">A-Z</option>
                  <option value="nDesc">Z-A</option>
              </optgroup>
              <optgroup label="Release">
                  <option value="rDesc">New</option>
                  <option value="rAsc">Old</option>
              </optgroup>
          </select>
        </div>
        <!-- [/Search Sort] -->
        <!-- [Card Body] -->
        <div class="flex flex-col h-full w-auto mt-4 lg:flex-row lg:flex-wrap md:flex-row md:flex-wrap justify-center">
          <!-- [CARDS] -->
          <div v-for="i in a()">
            <card :cardId="i.id" :cardLabel="i.name" :cardImg="i.img" :cardPrice="i.price" @click="$router.push({path: '/music/'+i.id})" />
          </div>
          <!-- [/CARDS] -->
        </div>
        <!-- [/Card Body] -->
      </div>
      <!-- [/MidField] -->
    </div>
    <!-- [/Body] -->
  </div>
  <!-- [/Screen] -->
  <!-- [Footerbar] -->
  <footerbar></footerbar>
  <!-- [/FooterBar] -->
</div>
</template>

<script setup>
  let apiData = ref([])
  apiData = await (await fetch("http://localhost:3030/music")).json()
  let searchTxt = ref('')
  let sortMode = ref('default')
  const a = () => {
    if (sortMode.value == "default" && searchTxt.value != "") {return apiData.filter(i => i.name.toLowerCase().includes(searchTxt.value.toLowerCase()) ) }
    else if (searchTxt.value == "" && sortMode.value != "default") {
      //chep-expensive 
      if (sortMode.value[0] == "p") {
        let va = []
        for (let i in apiData) {
          if(!va.includes(apiData[i])){ va.push(parseInt(apiData[i].price)) }
        }
        let r = []
        for (let i in va.sort((a,b)=>a-b)) {
          for (let j in apiData) {if (apiData[j].price == va[i] ) { r.push(apiData[j]) }}
        }
        if (sortMode.value == "pAsc") {return r} else return r.reverse()
      }
      //Name 
      if (sortMode.value[0] == "n") {
        let va = []
        for (let i in apiData) {
          if(!va.includes(apiData[i])){ va.push(apiData[i].name) }
        }
        let r = []
        for (let i in va.sort()) {
          for (let j in apiData) {if (apiData[j].name == va[i] ) { r.push(apiData[j]) }}
        }
        if (sortMode.value == "nAsc") {return r} else return r.reverse()
      }
      //Old-new 
      if (sortMode.value[0] == "r") {
        let r = []
        for (let i in apiData) { r.push(apiData[i]) }
        if (sortMode.value == "rDesc") {return r} else return r.reverse();
      }
    }
    else {return apiData.filter(i => i.name.toLowerCase().includes(searchTxt.value.toLowerCase()) )}
  }
</script>

<style>

</style>