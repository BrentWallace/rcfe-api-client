<template>
  <b-row>
    <b-col>
      <hr />
      <h2 class="mb-4 p-3 bg-secondary text-light">Search Summary</h2>
      <p><strong>Filters Applied <b-icon icon="filter-left"></b-icon></strong></p>
      <ul class="list-unstyled">
        <li v-for="(value, key) in filters" :key="key">{{ key }} - {{ value }}</li>
      </ul>
      <p>
        <strong>Total number of communities in search:</strong>
        {{ totalCommunities }}
      </p>
      <p>
        <strong>Total licensed beds in search:</strong>
        {{ totalCapacity }}
      </p>
      <hr />
    </b-col>
  </b-row>
</template>

<script>
export default {
  props: ["results", "filters"],
  computed: {
    totalCommunities: function() {
      return this.results.length;
    },
    totalCapacity: function() {
      let bedCount = 0;
      for (let community of this.results) {
        bedCount += parseInt(community["Facility Capacity"]);
      }
      return bedCount;
    }
  }
};
</script>

<style scoped>
</style>