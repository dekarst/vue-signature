<template>
  <div id="app">
    <Signature />
  </div>
</template>

<script>
import Signature from './components/Signature.vue'

export default {
  name: 'App',
  components: {
    Signature
  }
}
</script>

<style>
#app {
  font-family: Times New Roman, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
