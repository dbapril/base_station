<template>
  <div id="app">
    <BaseStation />
  </div>
</template>

<script>
import BaseStation from "./components/BaseStation.vue";

export default {
  name: "App",
  components: {
    BaseStation,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
