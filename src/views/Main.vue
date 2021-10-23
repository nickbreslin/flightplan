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
    <div
      class="col-3 border-bottom mb-3 pb-3"
      v-for="city in orderByLat"
      :key="city.iso2"
    >
      <img :src="getFlag(city.iso2)" style="width: 100px" />
      <p>{{ city.city }} ({{ city.country }})<br />({{ city.lat }})</p>
      <p v-for="route in city.routes" :key="route.city">
        ROUTE: {{ route.city }}
      </p>
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
    findClosestRoute(city) {
      let possible = this.orderByLat.filter(
        (capital) => parseFloat(capital.lat) > parseFloat(city.lat)
      );

      possible = possible.filter((capital) => {
        let alreadyARoute = city.routes.filter(
          (route) => route.city == capital.city
        );

        if (alreadyARoute.length) {
          return false;
        }

        return true;
      });

      return { ...possible[0] };
    },
  },
  mounted() {
    this.capitals = this.capitals.map((city) => {
      city.routes = [];
      city.routes.push(this.findClosestRoute(city));
      city.routes.push(this.findClosestRoute(city));
      city.routes.push(this.findClosestRoute(city));
      city.routes.push(this.findClosestRoute(city));

      return city;
    });
  },
};
</script>
