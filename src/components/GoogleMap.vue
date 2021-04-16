<template>
  <div>
    <GmapMap
      ref="mapRef"
      :center='center'
      :zoom='12'
      style='width:100vw;  height:100vh;'
    />
     <GmapMarker
        :key="index"
        v-for="(m, index) in markers"
        :position="m.position"
        @click="center=m.position"
      />
  </div>
</template>

<script>
export default {
  name: 'GoogleMap',
  data() {
    return {
      center: { lat: 45.508, lng: -73.587 },
      // currentPlace: null,
      markers: [],
      places: [],
    }
  },
  mounted() {
    this.geolocate();
    // this.addMarker();
  },
  methods: {
    // setPlace(place) {
    //   this.currentPlace = place;
    // },
    addMarker() {
      // if (this.currentPlace) {
        // const marker = {
        //   lat: this.center.lat,
        //   lng: this.center.lng,
        // };
        // this.places.push(this.currentPlace);
        // this.$refs["mapRef"].$mapPromise.then((map) => {
        //   marker.setMap(map);
        // });
        // this.markers.push(marker);
        //this.center = marker;
        //this.currentPlace = null;
      // }
    },
    geolocate: function() {
      navigator.geolocation.getCurrentPosition(position => {
        this.center = {
          lat: position.coords.latitude,
          lng: position.coords.longitude,
        };
      });
    },
  },
  
}
</script>