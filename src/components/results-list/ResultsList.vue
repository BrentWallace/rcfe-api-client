<template>
  <b-row class="mt-4">
    <b-col>
      <b-card-group columns>
        <app-result-card v-for="result in results" :key="result['_id']" :result="result"></app-result-card>
      </b-card-group>
    </b-col>
  </b-row>
</template>

<script>
import ResultCard from './ResultCard.vue'

export default {
  props: ["results"],
  components: {
    appResultCard: ResultCard,
  }
};
</script>

<style scoped>
</style>