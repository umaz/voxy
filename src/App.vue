<template>
  <div id="app">
    <v-app>
      <Voxy/>
    </v-app>
  </div>
</template>

<script>
import Voxy from './components/Voxy'

export default {
  name: 'App',
  components: {
    Voxy
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
