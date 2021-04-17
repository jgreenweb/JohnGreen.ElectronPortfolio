<template>
  <div id="QrContainerContainer">
    <QrContainer name="John Green" />
    <QrContainer
      v-for="coin in prices"
      v-bind:key="coin.id"
      :name="coin.name"
      :price="coin.price"
      :logo="coin.logo_url"
    />
  </div>
  <div id="button-container">
    <button class="btn btn-primary" v-on:click="getPrices()">Manual Price Fetch</button>
    <button class="btn btn-secondary" v-on:click="toggleFetching()">Auto Fetch: {{!pauseFetching}}</button>
  </div>
</template>

<script>
import QrContainer from "./components/QrContainer";
import axios from "axios";

export default {
  name: "App",
  components: {
    QrContainer,
  },
  data() {
    return {
      prices: [],
      message: "hello",
      pauseFetching: false
    };
  },
  methods: {
    testConnection() {
      this.prices = [1, 2, 3, 4];
      console.log(this.prices);
    },
    getPrices() {
      axios
        .get(
          "https://api.nomics.com/v1/currencies/ticker?key=b93ea7cd18ab1ab1d9af9129ad36a345&ids=XTZ,BURST,ADA"
        ) //need to set this in process env instead of hardcode
        .then((response) => {
          console.log(response);
          this.prices = response.data;
          console.log(this.prices)
        });
    },
    toggleFetching () {
      this.pauseFetching = !this.pauseFetching
    }
  },
  mounted() {
    this.getPrices();
    window.setInterval(() => {
      if(!this.pauseFetching) {
        this.getPrices()
      }
    }, 10000)
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 2rem;
  background-color: white;
}
#QrContainerContainer {
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  max-width: 40rem;
}
#button-container {
  display: flex;
  flex-direction: column;
}
button {
  margin: .5rem auto;
  background-color: goldenrod;
  max-width: 15rem;
}
</style>
