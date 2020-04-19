<template>
  <div id="app">
    <Map></Map>
  </div>
</template>

<script>
import Map from "./components/Map.vue";

export default {
  name: "App",
  components: {
    Map,
  },
};
</script>

<style>
html,
body {
  padding: 0px;
  margin: 0px;
}
</style>
