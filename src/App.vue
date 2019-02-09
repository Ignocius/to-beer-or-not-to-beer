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
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.55) 0%, rgba(144, 135, 135, 0.22) 39%, rgb(255, 255, 255) 75%, rgba(0, 0, 0, 0.11) 94%, rgba(0, 0, 0, 0.11) 100%);
  height: 100vh;
  width: 100vw;
}
</style>
