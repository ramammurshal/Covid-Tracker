<template>
  <div class="grid md:grid-cols-2 gap-4">
    <!-- box-1: cases -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Cases</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberWithCommas(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithCommas(stats.TotalConfirmed) }}
      </div>
    </div>
    <!-- ./box-1: cases -->

    <!-- box-2: deaths -->
    <div class="shadow-md bg-blue-100 p-10 text-center rounded">
      <h3 class="text-3xl text-blue-900 font-bold mb-4">Deaths</h3>
      <div class="text-2xl mb-4">
        <span class="font-bold">New:</span>
        {{ numberWithCommas(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Total:</span>
        {{ numberWithCommas(stats.TotalDeaths) }}
      </div>
    </div>
    <!-- ./box-2: deaths -->
  </div>
</template>

<script>
export default {
  name: 'DataBoxes',
  props: ['stats'],
  methods: {
    numberWithCommas(num) {
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    }
  }
}
</script>
