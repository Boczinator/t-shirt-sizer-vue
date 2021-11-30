<template>
  <div id="app">
    <SizerItem />
  </div>
</template>

<script>
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
  margin-top: 60px;
}
</style>
