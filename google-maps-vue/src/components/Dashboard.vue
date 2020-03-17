<template>
  <!--<div id="map"></div>-->
  <GmapMap
  :center="{lng: -87.665, lat: 41.867}"
  :zoom="16"
  map-type-id="terrain"
  style="width: 500px; height: 300px"
>
  <GmapMarker
    :key="index"
    v-for="(m, index) in markers"
    :position="m.position"
    :clickable="true"
    :draggable="true"
    @click="center=m.position"
  />
</GmapMap>
</template>

<script>
export default {
  name: 'Dashboard',
  props: {
    msg: String
  },
  data: function () {
    return {
      markers: [
        {position: {lng: -87.6649857, lat: 41.8690738}},
        {position: {lng: -87.6648952, lat: 41.8690754}},
        {position: {lng: -87.6648825, lat: 41.8694949}},
        {position: {lng: -87.664821, lat: 41.873856}},
        {position: {lng: -87.6648002, lat: 41.8690782}},
        {position: {lng: -87.6647942, lat: 41.8694922}},
        {position: {lng: -87.6647903, lat: 41.8718445}},
        {position: {lng: -87.6647069, lat: 41.8694913}},
        {position: {lng: -87.6647032, lat: 41.8690806}},
        {position: {lng: -87.6646183, lat: 41.8690946}},
        {position: {lng: -87.6645272, lat: 41.8690723}},
        {position: {lng: -87.664521, lat: 41.8723198}},
        {position: {lng: -87.6645206, lat: 41.8719059}},
        {position: {lng: -87.6645124, lat: 41.8722341}},
        {position: {lng: -87.66448, lat: 41.872642}},
        {position: {lng: -87.6644757, lat: 41.872697}},
        {position: {lng: -87.6644596, lat: 41.87249}},
        {position: {lng: -87.6644326, lat: 41.8690798}},
        {position: {lng: -87.6644178, lat: 41.8719134}},
        {position: {lng: -87.6643425, lat: 41.8690971}},
        {position: {lng: -87.6643289, lat: 41.8719093}},
        {position: {lng: -87.6642436, lat: 41.8695487}},
        {position: {lng: -87.6642419, lat: 41.8690612}},
        {position: {lng: -87.663973, lat: 41.8726416}},
        {position: {lng: -87.6639715, lat: 41.8722495}},
        {position: {lng: -87.6639605, lat: 41.871905}},
        {position: {lng: -87.6639305, lat: 41.873117}},
        {position: {lng: -87.663926, lat: 41.8694948}},
        {position: {lng: -87.6639011, lat: 41.8691054}},
        {position: {lng: -87.663886, lat: 41.8697116}},
        {position: {lng: -87.6638559, lat: 41.8709124}},
        {position: {lng: -87.6638536, lat: 41.8707727}},
        {position: {lng: -87.6638527, lat: 41.8708416}},
        {position: {lng: -87.6638519, lat: 41.8709847}},
        {position: {lng: -87.6638506, lat: 41.8710445}},
        {position: {lng: -87.6638446, lat: 41.8699563}},
        {position: {lng: -87.6638443, lat: 41.8698501}},
        {position: {lng: -87.6638418, lat: 41.8688549}},
        {position: {lng: -87.6638406, lat: 41.8707093}},
        {position: {lng: -87.6638397, lat: 41.8711199}},
        {position: {lng: -87.663834, lat: 41.8700229}},
        {position: {lng: -87.6638257, lat: 41.8706341}},
        {position: {lng: -87.6638096, lat: 41.8703632}}
      ]
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#map {
        height: 100%;
      }

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>