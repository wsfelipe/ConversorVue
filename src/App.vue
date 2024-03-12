<template>
  <div id="app">
    <ConversorComponente moeda-a="USD" moeda-b="BRL" />
  </div>
</template>

<script>
import ConversorComponente from "./components/ConversorComponente.vue";
export default {
  name: 'app',
  components: {
    ConversorComponente
  }
};
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
