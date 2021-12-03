
<template>
<div ref="leaflet">
<no-ssr>
    <l-map :zoom="zoom" :center="center">
        <l-tile-layer :url="url"/>
        <l-marker :lat-lng="marker"/>
        <l-icon-default :image-path="path"/>
    </l-map>
</no-ssr>

</div>

</template>

<script>
let Vue2Leaflet = {}
    if (process.client)
        Vue2Leaflet = require('vue2-leaflet')
import 'leaflet/dist/leaflet.css';
export default {
 components: {
          'l-map': Vue2Leaflet.LMap,
          'l-tile-layer': Vue2Leaflet.LTileLayer,
          'l-marker': Vue2Leaflet.LMarker
 },
 data () {
   return {
     zoom: 14,
                path: '/images/',
                center: [47.413220, -1.219482],
                url: 'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
                marker: (process.client)?L.latLng(47.413220, -1.219482):null,
   }
 },
 methods: {
   zoomUpdated (zoom) {
     this.zoom = zoom;
     console.log(this.markers)
   },
   centerUpdated (center) {
     this.center = center;
   }
 }
}
</script>

<style>
 .map {
   position: absolute;
   width: 100%;
   height: 100%;
   overflow :hidden
 }
</style>