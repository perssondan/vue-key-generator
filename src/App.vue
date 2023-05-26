<template>
  <div style="width: 50%; display: inline-grid;">
    <KeyGen />
  </div>
</template>

<script>
import KeyGen from './components/KeyGen.vue'

export default {
  name: 'App',
  components: {
    KeyGen
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
