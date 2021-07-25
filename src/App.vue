<template>
  <div id="app">
    <Cnpjs/>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Cnpjs from './components/Cnpjs.vue'
//<HelloWorld msg="Welcome to Your Vue.js App"/>
//HelloWorld
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
  color: #2c3e50;
  margin-top: 60px;
}
</style>
