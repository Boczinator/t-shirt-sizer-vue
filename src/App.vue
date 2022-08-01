<template>
  <div id="app">
    <div class="h-screen bg-red">
      <div class="flex flex-wrap justify-end w-full">
        <div class="w-10/12">
          <h1 class="text-3xl font-bold py-6">Awesome T-Shirt Sizer</h1>
          <div class="w-full mb-8">Stromberg says: {{ strombergQuote }}</div>
        </div>
        <img class="rounded-bl-full w-2/12 object-cover" src="../src/assets/images/team-webshop.jpeg" />
      </div>
      <SizerItem />
    </div>
  </div>
</template>

<script>
import './assets/css/tailwind.css';
import SizerItem from './components/SizerItem.vue';
import axios from "axios";

export default {
  name: 'App',
  components: {
    SizerItem
  },
  data() {
    return {
      strombergQuote: '',
    }
  },
  methods: {
    getStrombergQuote() {
      axios.get('https://www.stromberg-api.de/api/quotes/random')
          .then(response => {
            this.strombergQuote = response.data.quote
          });
    }
  },
  mounted() {
    this.getStrombergQuote();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
