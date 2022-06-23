<template>
  <!-- main -->
  <main v-if="!loading" class="pb-10">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountrySelect :countries="countries" @get-country="getCountryData" />
    <button 
      class="bg-green-700 text-white rounded-lg p-3 mt-7 hover:bg-green-800"
      v-if="stats.Country"
      @click="backGlobal"
    >
      Global
    </button>
  </main>
  <!-- ./main -->

  <!-- loading -->
  <main v-else class="flex align-center justify-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="Loading Image">
  </main>
  <!-- ./loading -->
</template>

<script>
import DataTitle from '../components/DataTitle.vue';
import DataBoxes from '../components/DataBoxes.vue';
import CountrySelect from '../components/CountrySelect.vue';

export default {
  name: 'Home',
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif'),
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();

      // console.log(data);
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async backGlobal() {
      this.loading = true;
      const data = await this.fetchCovidData();

      this.title = 'Global';
      this.stats = data.Global;
      this.loading = false;
    }
  },
  async created() {
    const data = await this.fetchCovidData();
    
    setTimeout(() => {
      this.dataDate = data.Date;
      this.stats = data.Global;
      this.countries = data.Countries;
      this.loading = false;
    }, 1000);
  }
}
</script>
