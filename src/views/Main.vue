<template>
  <div class="container-fluid">
    <div class="alert alert-secondary mt-3 text-center shadow">
      <h1 class="text-uppercase m-0">Flight Plan</h1>
    </div>

    <div class="row">
      <div class="col-sm-8">
        <div class="alert alert-success mb-3 text-center shadow">
          <h2 class="text-uppercase m-0">Game Board</h2>
        </div>
        <div class="alert alert-secondary mb-3 text-center shadow">
          <h2 class="text-uppercase m-0">instructions</h2>
        </div>
      </div>
      <div class="col-sm-4">
        <div class="card shadow mb-3 shadow">
          <div class="card-header h3 text-uppercase text-center">planes</div>
          <div class="card-body text-center"></div>
        </div>
        <div class="card shadow mb-3 shadow">
          <div class="card-header h3 text-uppercase text-center">
            Available Destinations
          </div>
          <div class="card-body text-center"></div>
        </div>
      </div>
    </div>
  </div>
  <div class="row">
    <div class="col-3" v-for="city in orderByLat" :key="city.iso2">
      <p>{{ city.city }} ({{ city.country }})<br />({{ city.lat }})</p>
      <img :src="getFlag(city.iso2)" style="width: 100px" />
    </div>
  </div>
</template>

<script>
import capitals from "@/data/worldcapitals.json";

export default {
  name: "Main",
  components: {},
  data: function () {
    return {
      capitals: capitals,
    };
  },
  computed: {
    orderByLat() {
      let toOrder = this.capitals;
      let ordered = toOrder.sort((a, b) =>
        parseFloat(a.lat) > parseFloat(b.lat) ? 1 : -1
      );
      return ordered;
    },
  },
  methods: {
    getFlag(iso2) {
      let path = "";
      try {
        path = require(`@/assets/svg/${iso2}.svg`);
      } catch (error) {
        console.log("No Flag", iso2);
      }
      return path;
    },
  },
};
</script>
