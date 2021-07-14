<template>
  <main v-if="!loading">
    <data-title :text="title" :dataDate="dataDate" />
    <country-select
      @get-country="getCountryData"
      @set-global="clearCountryData"
      :countries="countries"
    />
    <data-boxes :stats="stats" />
  </main>
  <main class="flex flex-col alogn-center justify-ceenter text-center" v-else>
    <!--   <img :src="loadingImage" class="w-24 m-auto" alt="" />-->
    <loading />
  </main>
</template>

<script>
import CountrySelect from "../components/CountrySelect.vue";
import DataBoxes from "../components/DataBoxes.vue";
import DataTitle from "../components/DataTitle.vue";
import Loading from "../components/Loading.vue";
export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
    Loading,
  },
  data() {
    return {
      title: "Global",
      loading: true,
      dataDate: "",
      status: {},
      countries: [],
      loadingImage: require("../assets/Hourglass.gif"),
      posts: ["Saab", "Volvo", "BMW"],
    };
  },

  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary");
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.stats = data.Global;
      this.title = "Global";
      this.loading = false;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
    console.log(this.countries[0].Country);
  },
};
</script>
