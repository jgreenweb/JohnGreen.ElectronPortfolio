<template>
  <div class="card QrContainer">
    <img class= "card-img-top" :src="logo ? logo : myFace"/>
    <h4 class="card-body">{{ price ? price : name }}</h4> 
    <canvas v-on:click="getProps" class="card-img-bottom" v-bind:id="name" width="100" height="100"/>
  </div>

</template>

<script>
const QRCode = require('qrcode')
export default {
  name: "QrContainer",
  props: ['name', 'price', 'logo'],
  data() {
    return {
      myFace: "https://media-exp1.licdn.com/dms/image/C4D03AQG8srAfhWbhhg/profile-displayphoto-shrink_800_800/0/1605154329795?e=1623888000&v=beta&t=Igj-4KwBvZuH5k1DRf48IWZJ-h-W7zW1DIFnzocmC_E"
    }
  },
  methods: { 
    getProps () {
      console.log(this.name, this.price, this.logo)
    },
    generateQr () {
      let text = this.price ? this.price : this.name //uses the price prop if it exists, otherwise defaults to name prop
      const container = document.getElementById(this.name)
      QRCode.toCanvas(container, text, { errorCorrectionLevel: 'L' }, (err) => {
        if (err) throw err
      })
    }
  },
  updated() {
    console.log("updated!")
    this.generateQr()
  },
  mounted() {
    this.generateQr()
  }
}
</script>

<style scoped>
  .QrContainer {
    display: block;
    margin: 0 .5rem .5rem
  }
  h4 {
    font-size: 1.2rem;
    margin-bottom: -1rem;
  }
  img {
    max-height: 3rem;
    max-width: 3.5rem;
    margin-top: 1rem;
  }
</style>