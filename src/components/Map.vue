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
  data() {
    return {
      data: [],
      osmMap: {},
      select: {
        city: "桃園市",
        town: "中壢區",
      },
    };
  },
  mounted() {
    // console.log(document.getElementById("map"));
    //設定地圖位子在center zoom在 15
    this.osmMap = L.map("map", {
      center: [24.99, 121.3],
      zoom: 15,
    });
    //引入地圖放到id map的dom裡面
    L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
      attribution: '<a target="_blank" href="https://www.openstreetmap.org/">© OpenStreetMap 貢獻者</a>',
      maxZoom: 18,
    }).addTo(this.osmMap);
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
        // console.log(r.data.features);
        this.data = r.data.features;
      });
      this.update();
    },
    update() {
      const result = this.data.filter((e) => e.properties.county == "桃園市");
      console.log(result);
      result.forEach((e) => {
        L.marker([e.geometry.coordinates[1], e.geometry.coordinates[0]]).addTo(this.osmMap);
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
