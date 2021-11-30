<template>
  <div id="app">
    <div class="h-screen bg-red">
      <h1 class="text-3xl font-bold py-6">Awesome T-Shirt Sizer</h1>
      <SizerItem />
    </div>
  </div>
</template>

<script>
import './assets/css/tailwind.css';
import SizerItem from './components/SizerItem.vue';

export default {
  name: 'App',
  components: {
    SizerItem
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
