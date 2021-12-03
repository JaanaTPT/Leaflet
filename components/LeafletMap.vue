<template>
<div>
<no-ssr>
    <l-map :zoom="zoom" :center="center" :geoJson="covidGeoJson" :mapStyle="style" :key="styleProperty" ref="leaflet" class="leaflet" >
        <l-tile-layer :url="url"/>
        <l-geo-json :geojson="geojson"></l-geo-json>
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
  //  props: ['center', 'zoom','geoJson', 'mapStyle'],

    components: {
        'l-map': Vue2Leaflet.LMap,
        'l-tile-layer': Vue2Leaflet.LTileLayer,
        'l-geo-json': Vue2Leaflet.LGeoJson,
        },
    data() {
        return {
            zoom: 4,
            center: [44, 24],
            url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
            geojson: null,
            }
        },
    watch: {
        center(newCenter){
            this.map.panTo(newCenter);
        },
        zoom(newZoom){
            this.map.setZoom(newZoom);
        },
        geoJson(geoJson){
            this.map.data.addGeoJson(geoJson);
        },
        mapStyle(mapStyle){
            console.log('setStyle');
            this.map.data.setStyle(mapStyle);
        }
    },
    async created() {
        const response = await fetch('https://raw.githubusercontent.com/johan/world.geo.json/master/countries.geo.json');
        this.geojson = await response.json();
    },
}
</script>

<style scoped>
    div {
        height: 800px;
    }
</style>