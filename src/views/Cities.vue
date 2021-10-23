<template>
  <vue-csv-import
    v-model="citiesCSV"
    :fields="{
      city: { label: 'city' },
      capital: { label: 'capital' },
      lat: { label: 'lat' },
      lng: { label: 'lng' },
      country: { label: 'country' },
      iso2: { label: 'iso2' },
      population: { label: 'population' },
    }"
  >
    <vue-csv-toggle-headers></vue-csv-toggle-headers>
    <vue-csv-errors></vue-csv-errors>
    <vue-csv-input></vue-csv-input>
    <vue-csv-map></vue-csv-map>
  </vue-csv-import>
  <div class="alert alert-danger">
    {{ formattedCities }}
  </div>
</template>

<script>
//import citiesCSV from "@/data/worldcities.csv";

import {
  VueCsvToggleHeaders,
  VueCsvMap,
  VueCsvInput,
  VueCsvErrors,
  VueCsvImport,
} from "vue-csv-import";

export default {
  name: "Cities",
  components: {
    VueCsvToggleHeaders,
    VueCsvMap,
    VueCsvInput,
    VueCsvErrors,
    VueCsvImport,
  },
  data: function () {
    return {
      citiesCSV: {},
    };
  },
  computed: {
    formattedCities() {
      if (this.citiesCSV.length) {
        return this.citiesCSV.filter((city) => city.capital == "primary");
      }
      return "";
    },
  },
};
</script>
