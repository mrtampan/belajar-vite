<template>
<div class="container mx-auto mt-4">
  <label class="block text-sm font-medium text-gray-700">Pilih Gambar</label>
    <select class="px-3 py-2 rounded border mb-4" @change="chooseCategory">
      <option value="">Pilih</option>
      <option value="happy">Happy</option>
      <option value="waifu">Waifu</option>
      <option value="neko">Neko</option>
      <option value="shinobu">Shinobu</option>
      <option value="megumin">Megumin</option>
      <option value="bully">Bully</option>
      <option value="cuddle">Cuddle</option>
      <option value="cry">Cry</option>
      <option value="hug">Hug</option>
      <option value="awoo">Awoo</option>
      <option value="kiss">Kiss</option>
      <option value="lick">Lick</option>
      <option value="pat">Pat</option>
      <option value="smug">Smug</option>
      <option value="bonk">Bonk</option>
      <option value="yeet">Yeet</option>
      <option value="blush">Blush</option>
      <option value="smile">Smile</option>
    </select>
    <!-- <input v-model="inputVal" type="text" placeholder="search" class="rounded border px-3 py-2 text-pink-500" />
    <button @click="submitSearch" class="bg-green-400 px-3 py-2 rounded text-white">Submit</button> -->
  <br/>
  <!-- <div class="grid grid-cols-1 md:grid-cols-3 md:gap-4">
    <div class="bg-red-400">1</div>
    <div class="bg-red-400">2</div>
    <div class="bg-red-400">3</div>
    <div class="bg-red-400">4</div>
    <div class="bg-red-400">5</div>
    <div class="bg-red-400">6</div>
    <div class="bg-red-400">7</div>
  </div> -->
        <modal v-if="modalShow" @close="modalShow = false">
        <template v-slot:header>Result</template>
        <template v-slot:body>
          <img :src="resultImage.url"/>
        </template>
        <template v-slot:footer>
          <button class="bg-blue-400 px-3 py-2 rounded mx-auto text-white" @click="modalShow = false">
            OK
          </button>
        </template>
      </modal>
</div>
</template>

<script>
import axios from 'axios'
import modal from './Modal.vue'
export default {
  name: 'HelloWorld',
  components:{
    modal
  },
  data() {
    return {
      count: 0,
      modalShow: false,
      inputVal: '',
      resultImage: ''
    }
  },
  methods:{
    chooseCategory(event){
      console.log(event.target.value)
      this.searchImage(event.target.value)
    },
    submitSearch(){

    axios.get('https://api.waifu.pics/sfw/' + this.inputVal).then((response) => {
      console.log(response.data)
    })

      this.modalShow = true
    },
    searchImage(valueInput){
      axios.get('https://api.waifu.pics/sfw/' + valueInput).then((response) => {
        this.resultImage = response.data
        this.modalShow = true
      })
    }
  }
}
</script>
