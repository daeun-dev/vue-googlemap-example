<template>
  <div>
    <GmapAutocomplete
        @place_changed='setPlace'
      />
    <button @click="addMarker">add</button>
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
// import { gmapApi } from 'vue2-google-maps'
export default {
  name: 'GoogleMap',
  data() {
    return {
      center: { lat: 45.508, lng: -73.587 },
      currentPlace: null,
      markers: [],
      places: []       
    }
  },
  mounted() {
    this.geolocate();
  },
  methods: { 
    setPlace(place) {
      this.currentPlace = place;
    },
    addMarker() {
      if (this.currentPlace) {
        const marker = {
          
          lat: this.currentPlace.geometry.location.lat(),
          lng: this.currentPlace.geometry.location.lng(),
        };
        this.markers.push({ position: marker });
        this.places.push(this.currentPlace);
        this.center = marker;
        this.currentPlace = null;
      }
    },
  //   // addMarker() {
  //   //     const marker = {
  //   //       lat: this.center.lat,
  //   //       lng: this.center.lng,
  //   //     };

  //   //     // this.google.maps.Map(this.$refs.mapRef);
  //   //     // const mapOptions = {
  //   //     //   zoom : 12,
  //   //     //  // center : { lat: 45.508, lng: -73.587 }
  //   //     // }
  //   //     // console.log(this.map);
  //   //     //document.getElementsByTagName("GmapMap")
  //   //     // this.map = GmapApi.maps.Map(this.$refs['mapRef], mapOptions);
  //   //     // const el = document.createElement("div");
  //   //     // const pointer = new CustomMaker(
  //   //     //   new this.google.maps.LatLng(this.center.lat,this.center.lng),el
  //   //     // )
  //   //     // console.log(marker.lat+", " +marker.lng);g
  //   //     // this.places.push(this.currentPlace);
  //   //     // console.log(map);
  //   //      this.$refs,mapRef.$mapPromise.then((map) => {
  //   //     // //   //  console.log(this.map);
  //   //         // marker.setMap(map);
  //   //     map.panTo({lat: 45.508, lng: -73.587})
  //   //     });
  //   //      // this.markers.push(marker);
  //   // },
    geolocate() {
      navigator.geolocation.getCurrentPosition(position => {
        this.center = {
          lat: position.coords.latitude,
          lng: position.coords.longitude,
        };
      });
    }
  }
};
</script>