<template>
  <div>
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
      keyNr: 30
    }
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
