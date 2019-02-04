<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <card-wrapper msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import CardWrapper from './components/CardWrapper.vue'

export default {
  name: 'app',
  components: {
    CardWrapper
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #e4e3e1;
  height: 100vh;
  width: 100vw;
}
</style>
