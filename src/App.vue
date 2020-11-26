<template>
  <div id="app">
    <mode></mode>
    <inputEnter></inputEnter>
  </div>
</template>

<script>

import mode from './mode'
import inputEnter from './inputEnter'
export default {
  name: 'App',
  components: {
   mode,
   inputEnter
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
