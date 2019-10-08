<template>
  <div id="app">
    <Calculator />
  </div>
</template>

<script>
import Calculator from "@/components/Calculator.vue";
export default {
  name: "app",
  components: {
    Calculator
  }
};
</script>

<style lang="scss">
$red: #ea6262;
html {
  min-width: 100vh;
  min-height: 100vh;
  font-family: "Overpass Mono", san-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: $red;
}
#app {
  text-align: center;
  margin-top: 60px;
  perspective: 3000px;
}
</style>
