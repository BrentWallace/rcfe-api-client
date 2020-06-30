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
      </table>
    </b-card-text>
  </b-card>
</template>

<script>
export default {
  props: ['result']
};
</script>

<style scoped>
</style>