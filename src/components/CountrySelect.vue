<template>
  <select 
    v-model="selected" 
    class="form-select mt-10 block w-full border-2 border-blue-200 p-3 rounded focus:outline-2 focus:outline-blue-400"
    @change="onChange"
  >
    <option value="0">Select Country</option>
    <option v-for="country in countries" :value="country.ID" :key="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'CountrySelect',
  props: ['countries'],
  data() {
    return {
      selected: 0,
    }
  },
  methods: {
    onChange() {
      const country = this.countries.find(country => country.ID === this.selected);

      this.$emit('get-country', country);
    }
  }
}
</script>
