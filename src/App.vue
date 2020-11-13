<template>
  <div id="app">
    <SimonMain />
  </div>
</template>

<script>
import SimonMain from "./components/SimonMain";

export default {
  name: "App",
  components: {
    SimonMain,
  },
};
</script>

<style>
html {
  box-sizing: border-box;
}
*,
*::before,
*::after {
  box-sizing: inherit;
}
#app {
  padding: 300px 100px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  position: relative;
}
</style>
