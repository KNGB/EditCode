<template>
  <div id="app">
    <mode></mode>
    <inputEnter></inputEnter>
    <canvasa></canvasa>
  </div>
</template>

<script>
import mode from "./mode";
import inputEnter from "./inputEnter";
import canvasa from "./canvas";
export default {
  name: "App",
  components: {
    mode,
    inputEnter,
    canvasa,
  },
};
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
