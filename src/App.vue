<template>
  <div id="app">
    <b-container>
      <app-header></app-header>
      <app-form @searchSubmitted="result = $event"></app-form>
      {{ result }}
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Form from './components/Form.vue'

export default {
  name: 'App',
  components: {
    appHeader: Header,
    appForm: Form,
  },
  data () {
    return {
      result: ''
    }
  }
}
</script>

<style>

</style>
