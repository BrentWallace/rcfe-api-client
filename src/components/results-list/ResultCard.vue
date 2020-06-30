<template>
  <b-card :title="result['Facility Name']">
    <b-card-text class="text-secondary">
      <table class="table table-borderless table-sm">
        <tr>
          <td>
            <b-icon icon="geo-alt"></b-icon>
          </td>
          <td>{{ result['Facility Address'] }} {{ result['Facility City'] }}, {{ result['Facility State'] }} {{ result['Facility Zip'] }}</td>
        </tr>
        <tr>
          <td>
            <b-icon icon="phone"></b-icon>
          </td>
          <td>{{ result['Facility Telephone Number'] }}</td>
        </tr>
        <tr>
          <td><b-icon icon="person-circle"></b-icon></td>
          <td>{{ result['Facility Capacity'] }}</td>
        </tr>
        <tr>
          <td>Status: </td>
          <td>{{ result['Facility Status'] }}</td>
        </tr>
        <tr>
          <td>First Licensed:</td>
          <td>{{ result['License First Date'] }}</td>
        </tr>
        <tr>
          <td><b-icon icon="link45deg"></b-icon></td>
          <td><a :href="link" target="_blank"><b-button variant="primary">Link to DSS Page</b-button></a></td>
        </tr>
      </table>
    </b-card-text>
  </b-card>
</template>

<script>
export default {
  props: ['result'],
  computed: {
    link: function() {
      const baseURL = 'https://www.ccld.dss.ca.gov/carefacilitysearch/FacDetail/';
      let facilityNumber = this.result['Facility Number'];

      if ( facilityNumber.length < 10 ) {
        facilityNumber = `0${facilityNumber}`;
      }

      return `${baseURL}${facilityNumber}`
    }
  }
}
</script>

<style scoped>
</style>