<template>
  <div id="app">
    <b-container>
      <app-header></app-header>
      <app-form @searchSubmitted="result = $event" @update:filters="filters = $event" @formReset="formReset()"></app-form>
      <app-search-summary v-if="result" :results="this.result" :filters="this.filters"></app-search-summary>
      <app-results-list :results="this.result"></app-results-list>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Form from './components/Form.vue'
import SearchSummary from './components/SearchSummary.vue'
import ResultsList from './components/results-list/ResultsList.vue'

export default {
  name: 'App',
  components: {
    appHeader: Header,
    appForm: Form,
    appSearchSummary: SearchSummary,
    appResultsList: ResultsList,
  },
  data () {
    return {
      result: '',
      filters: {}
    }
  },
  methods: {
    formReset: function () {
      this.result = '';
      this.filters = {}
    }
  }
}
</script>

<style>

</style>
