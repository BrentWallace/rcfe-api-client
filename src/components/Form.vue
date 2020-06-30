<template>
  <b-form @submit.prevent="onSubmit" @reset.prevent="onReset">
    <b-form-row>
      <b-col>
        <p class="bg-secondary text-light text-center p-2">Search Filters</p>
      </b-col>
    </b-form-row>
    <b-form-row>
      <b-col>
        <b-form-group label="Filter by City">
          <b-form-input v-model="filterCity"></b-form-input>
        </b-form-group>
        <b-form-group label="Filter by Zip">
          <b-form-input v-model="filterZip"></b-form-input>
        </b-form-group>
      </b-col>
      <b-col>
        <b-form-group label="Filter by RCFE#">
          <b-form-input v-model="filterNumber"></b-form-input>
        </b-form-group>
        <b-form-group label="Filter by Address">
          <b-form-input v-model="filterAddress"></b-form-input>
        </b-form-group>
      </b-col>
    </b-form-row>
    <b-form-row>
      <b-col>
        <b-button type="submit" variant="primary" class="mr-2">Submit</b-button>
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
      filterNumber: '',
      filterAddress: '',
      result: '',
      filters: {}
    };
  },
  methods: {
    onSubmit: async function() {
      const url = 'http://localhost:3000/communities'
      let queryString = ''

      if (this.filterCity) {
        this.filters.city = this.filterCity;
      }

      if (this.filterZip) {
        this.filters.zip = this.filterZip;
      }

      if (this.filterNumber) {
        this.filters.facilityNumber = this.filterNumber
      }

      if (this.filterAddress) {
        this.filters.address = this.filterAddress
      }

      for (let filter in this.filters) {
        queryString += `${filter}=${this.filters[filter]}&`;
      }

      const fetchedData = await fetch(`${url}?${queryString}`);
      this.result = await fetchedData.json();
      this.$emit('searchSubmitted', this.result);
      this.$emit('update:filters', this.filters);
    },
    onReset: function() {
      this.filterCity = '';
      this.filterZip = '';
      this.filterNumber = '';
      this.filterAddress = '';
      this.result = '';
      this.filters = {}
      this.$emit('formReset', this.result);
    }
  }
};
</script>

<style scoped>
</style>