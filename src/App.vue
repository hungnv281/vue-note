<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <ABC />
</template>

<script>
import ABC from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    ABC,
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
