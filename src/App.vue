<template>
  <div id="app">
    <card-wrapper msg="Welcome to Your Beer Finder"/>
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
