<template>
      <main v-if="!loading">
            <DataTitle :text="title" :dataDate="dataDate" />
            <DataBoxes :stats="stats" />
            <CountrySelect @get-country="getCountryData" :countries="countries" />
      </main>

      <main v-else class="flex flex-col align-center justify-center text-center">
            <div class="text-gray-500 text-3xl mt-10 mb-6">
                  <p>Fetching Data</p>
            </div>
            <img :src="loadingImage" class="w-80 m-auto" />
      </main>
</template>

<script>
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

export default {
      name: "HomeView",
      components: { DataTitle, DataBoxes, CountrySelect },
      data() {
            return {
                  loading: true,
                  title: "Global",
                  dataDate: "",
                  stats: {},
                  countries: [],
                  loadingImage: require("../assets/Ripple-1s-200px.gif"),
            };
      },
      methods: {
            async fetchCovidData() {
                  const response = await fetch("https://api.covid19api.com/summary");
                  const data = await response.json();
                  return data;
            },
            getCountryData(country) {
                  this.stats = country;
                  this.title = country.Country;
            },
      },
      async created() {
            const data = await this.fetchCovidData();
            console.log(data);
            this.dataDate = data.Date;
            this.stats = data.Global;
            this.countries = data.Countries;
            this.loading = false;
      },
};
</script>
