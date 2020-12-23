<template>
  <div id="app">
    <BaseStation :stationData="stationData" />
  </div>
</template>

<script>
import jsonData from "@/mocks/site.json";
import BaseStation from "./components/BaseStation.vue";

export default {
  name: "App",

  components: {
    BaseStation,
  },

  data() {
    return {
      stationData: jsonData,
    };
  },
};
</script>

<style>
@import url("./assets/css/reset.css");
@import url("./assets/css/fonts.css");
@import url("./assets/css/main.css");
</style>
