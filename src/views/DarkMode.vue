<script>
import Darkmode from "darkmode-js";

new Darkmode().showWidget();

/* global mapboxgl */
export default {
  data: function () {
    return {
      current_time: new Date(),
      darkmode: new Darkmode(),
      places: [
        { lat: -73.959025, lng: 40.70649, description: "Brooklyn Baby!" },
        { lat: -73.981793, lng: 40.767879, description: "Trump may have a tower here" },
        { lat: -73.95879542853694, lng: 40.78310572628607, description: "It's the Gu-gu-gugenheim" },
        { lat: -73.99247833505952, lng: 40.77022628730826, description: "Terminal 5, Live and Direct" },
        { lat: -74.01539230796661, lng: 40.703000470168085, description: "Battery PaRk" },
      ],
    };
  },
  mounted: function () {
    mapboxgl.accessToken = process.env.VUE_APP_MAP_AUTH_TOKEN;
    const map = new mapboxgl.Map({
      container: "map", // container ID
      style: "mapbox://styles/mapbox/streets-v11", // style URL
      center: [-73.929718, 40.626655], // starting position [lng, lat]
      zoom: 8, // starting zoom
    });
    // create the popup
    const popup = new mapboxgl.Popup({ offset: 25 }).setText("Lovingly known as Chi-Raq");
    const marker1 = new mapboxgl.Marker().setLngLat([-87.623177, 41.881832]).setPopup(popup).addTo(map);
    console.log(map);
    console.log(marker1);
    console.log(popup);
    this.places.forEach((place) => {
      const popup1 = new mapboxgl.Popup({ offset: 25 }).setText([place.description]);
      new mapboxgl.Marker().setLngLat([place.lat, place.lng]).setPopup(popup1).addTo(map);
      console.log(place);
    });
  },
  methods: {
    nightMode: function () {
      this.darkmode.toggle();
      console.log(date1.getUTCHours());
    },
  },
};
</script>

<template>
  <div class="map">
    <h2>Map Test</h2>
    <div id="map"></div>
    <button v-on:click="nightMode()">Nightmode</button>
  </div>
</template>

<style>
#map {
  width: 100%;
  height: 400px;
}
</style>
