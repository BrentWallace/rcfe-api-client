<template>
  <b-form @submit.prevent="onSubmit" @reset.prevent="onReset">
    <b-form-row>
      <b-col>
        <b-form-group label="Filter by City">
          <b-form-input v-model="filterCity"></b-form-input>
        </b-form-group>
        <b-form-group label="Filter by Zip">
          <b-form-input v-model="filterZip"></b-form-input>
        </b-form-group>
      </b-col>
    </b-form-row>
    <b-form-row>
      <b-col>
        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="secondary">Reset</b-button>
      </b-col>
    </b-form-row>
  </b-form>
</template>

<script>
export default {
  data() {
    return {
      filterCity: '',
      filterZip: '',
      result: ''
    };
  },
  methods: {
    onSubmit: async function() {
      const url = 'http://localhost:3000/communities'
      let filters = {}
      let queryString = ''

      if (this.filterCity) {
        filters.city = this.filterCity;
      }

      if (this.filterZip) {
        filters.zip = this.filterZip;
      }

      for (let filter in filters) {
        queryString += `${filter}=${filters[filter]}&`;
      }

      const fetchedData = await fetch(`${url}?${queryString}`);
      this.result = await fetchedData.json();
      this.$emit('searchSubmitted', this.result);
    },
    onReset: function() {
      this.filterCity = "";
      this.filterZip = "";
    }
  }
};
</script>

<style scoped>
</style>