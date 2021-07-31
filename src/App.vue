<template>
  <div id="app">
    <Cnpjs/>
  </div>
</template>

<script>

import Cnpjs from './components/Cnpjs.vue'

export default {
  name: 'App',
  components: {
    Cnpjs
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
