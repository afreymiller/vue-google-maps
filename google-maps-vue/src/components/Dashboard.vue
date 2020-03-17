<template>
  <!--<div id="map"></div>-->
  <GmapMap
  :center="{lat:-25, lng:130}"
  :zoom="10"
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
      markers: [{
        position: {lat: -25.363, lng: 131.044}
      }, {
        position: {lat: -24, lng: 132}
      }]
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