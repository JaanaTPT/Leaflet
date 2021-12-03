
<template>
<div>
<no-ssr>
    <l-map :zoom="zoom" :center="center" ref="leaflet" class="leaflet" >
        <l-tile-layer :url="url"/>
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
        },
    data() {
        return {
            zoom: 4,
            center: [44, 24],
            url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
            }
        },
}
</script>

<style scoped>
    div {
        height: 800px;
    }
</style>