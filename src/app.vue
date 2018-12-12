<template>
  <div id="app">
    <Datashow/>
  </div>
</template>

<script>
import Datashow from './components/Datashow.vue'

export default {
  name: 'App',
  components: {
    Datashow
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
  margin-top: 0px;
}
</style>
