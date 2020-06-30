<template>
  <b-row>
    <b-col>
      <GmapMap
        :center="center"
        :zoom="6"
        map-type-id="terrain"
        style="width: 100%; height: 600px;"
      >
        <gmap-info-window
          :options="infoWindowOptions"
          :position="infoWindowPos"
          :opened="infoWindowOpen"
          @closeclick="infoWindowOpen=false"
        ></gmap-info-window>
        <GmapMarker
          :key="index"
          v-for="(m, index) in this.results"
          :position="{ lat:parseFloat(m.Latitude), lng:parseFloat(m.Longitude) }"
          :title="m['Facility Name']"
          :clickable="true"
          @click="toggleInfoWindow(m,index)"
        />
      </GmapMap>
    </b-col>
  </b-row>
</template>

<script>
export default {
  props: ["results"],
  data() {
    return {
      center: {
        lat: 36,
        lng: -120,
      },
      infoWindowPos: null,
      infoWindowOpen: false,
      infoWindowOptions: {
        content: "",
        pixelOffset: {
          width: 0,
          height: -35
        }
      },
      currentMarkerIndex: null
    };
  },
  methods: {
    toggleInfoWindow: function(marker, index) {
      const latitude = parseFloat(marker.Latitude)
      const longitude = parseFloat(marker.Longitude)
      
      this.center = {lat: latitude, lng: longitude}
      this.infoWindowPos = {
        lat: latitude,
        lng: longitude
      };
      this.infoWindowOptions.content = `<span class="h5">${marker["Facility Name"]}</span>`

      if (this.currentMarkerIndex == index) {
        this.infoWindowOpen = !this.infoWindowOpen;
      } else {
        (this.infoWindowOpen = true), (this.currentMarkerIndex = index);
      }
    }
  }
};
</script>

<style scoped>
</style>