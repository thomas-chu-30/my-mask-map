<template>
  <div class="map">
    <div class="height"></div>
    <div class="height" id="map"></div>
  </div>
</template>

<script>
import L from "leaflet";
console.log(L);
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  beforeMount() {
    console.log(document.getElementById("map"));
  },
  mounted() {
    console.log(document.getElementById("map"));
    const osmMap = L.map("map", {
      center: [25.03, 121.55],
      zoom: 15,
    });
    L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
      attribution: '<a target="_blank" href="https://www.openstreetmap.org/">© OpenStreetMap 貢獻者</a>',
      maxZoom: 18,
    }).addTo(osmMap);
    console.log("osmap end");
  },
  created() {
    console.log("created start");
    this.getData();
    console.log("get Data end");
    //
    console.log("created end");
  },
  methods: {
    async getData() {
      console.log("get Data strat");
      await this.axios.get("https://raw.githubusercontent.com/kiang/pharmacies/master/json/points.json").then((r) => {
        console.log(r.data.features);
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
  border: 1px solid;
}
.map {
  display: grid;
  grid-template-columns: 25% 75%;
}
.height {
}
#map {
  height: 400px;
  height: 100vh;
}
</style>
