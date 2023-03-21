<template>
  <div class="container">
  <h2>Transformer input</h2>
    <TxtSwitch
      v-model="text"
      :switchThreshold="keyNr"
    />
  </div>
</template>

<script>
import TxtSwitch from './components/TxtSwitch.vue'

export default {
  name: 'App',
  components: {
    TxtSwitch
  },
  data() {
    return{
      keyNr: 16
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>