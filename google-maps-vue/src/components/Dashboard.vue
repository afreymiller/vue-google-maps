<template>
<div>
  <GmapMap
  :center="{lng: -87.665, lat: 41.867}"
  :zoom="16"
  map-type-id="terrain"
  style="width: 500px; height: 300px"
>
  <gmap-info-window :options="infoOptions" :position="infoWindowPos" :opened="infoWinOpen" @closeclick="infoWinOpen=false">
  </gmap-info-window>
  <GmapMarker
    :key="index"
    v-for="(m, index) in markers"
    :position="m.position"
    :clickable="true"
    :draggable="true"
    @click="toggleInfoWindow(m,index)"
  />
</GmapMap>
<select v-model="selected">
  <option v-for="option in options" v-bind:key="option.text" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selected: {{ selected }}</span>
</div>
</template>

<script>
export default {
  name: 'Dashboard',
  props: {
    msg: String
  },
  data: function () {
    return {
      selected: 'A',
      options: [
        { text: 'One', value: 'A' },
        { text: 'Two', value: 'B' },
        { text: 'Three', value: 'C' }
      ],
      infoWindowPos: null,
      infoWinOpen: false,
      currentMidx: null,
      infoOptions: {
        content: '',
          //optional: offset infowindow so it visually sits nicely on top of our marker
        pixelOffset: {
          width: 0,
          height: -35
        }
      },
      markers: [
        {position: {lng: -87.6649857, lat: 41.8690738}, infoText: 'Marker 1'},
        {position: {lng: -87.6648952, lat: 41.8690754}, infoText: 'Marker1'},
        {position: {lng: -87.6648825, lat: 41.8694949}, infoText: 'Marker1'},
        {position: {lng: -87.664821, lat: 41.873856}, infoText: 'Marker1'},
        {position: {lng: -87.6648002, lat: 41.8690782}, infoText: 'Marker1'},
        {position: {lng: -87.6647942, lat: 41.8694922}, infoText: 'Marker1'},
        {position: {lng: -87.6647903, lat: 41.8718445}, infoText: 'Marker1'},
        {position: {lng: -87.6647069, lat: 41.8694913}, infoText: 'Marker1'},
        {position: {lng: -87.6647032, lat: 41.8690806}, infoText: 'Marker1'},
        {position: {lng: -87.6646183, lat: 41.8690946}, infoText: 'Marker1'},
        {position: {lng: -87.6645272, lat: 41.8690723}, infoText: 'Marker1'},
        {position: {lng: -87.664521, lat: 41.8723198}, infoText: 'Marker1'},
        {position: {lng: -87.6645206, lat: 41.8719059}, infoText: 'Marker1'},
        {position: {lng: -87.6645124, lat: 41.8722341}, infoText: 'Marker1'},
        {position: {lng: -87.66448, lat: 41.872642}, infoText: 'Marker1'},
        {position: {lng: -87.6644757, lat: 41.872697}, infoText: 'Marker1'},
        {position: {lng: -87.6644596, lat: 41.87249}, infoText: 'Marker1'},
        {position: {lng: -87.6644326, lat: 41.8690798}, infoText: 'Marker1'},
        {position: {lng: -87.6644178, lat: 41.8719134}, infoText: 'Marker1'},
        {position: {lng: -87.6643425, lat: 41.8690971}, infoText: 'Marker1'},
        {position: {lng: -87.6643289, lat: 41.8719093}, infoText: 'Marker1'},
        {position: {lng: -87.6642436, lat: 41.8695487}, infoText: 'Marker1'},
        {position: {lng: -87.6642419, lat: 41.8690612}, infoText: 'Marker1'},
        {position: {lng: -87.663973, lat: 41.8726416}, infoText: 'Marker1'},
        {position: {lng: -87.6639715, lat: 41.8722495}, infoText: 'Marker1'},
        {position: {lng: -87.6639605, lat: 41.871905}, infoText: 'Marker1'},
        {position: {lng: -87.6639305, lat: 41.873117}, infoText: 'Marker1'},
        {position: {lng: -87.663926, lat: 41.8694948}, infoText: 'Marker1'},
        {position: {lng: -87.6639011, lat: 41.8691054}, infoText: 'Marker1'},
        {position: {lng: -87.663886, lat: 41.8697116}, infoText: 'Marker1'},
        {position: {lng: -87.6638559, lat: 41.8709124}, infoText: 'Marker1'},
        {position: {lng: -87.6638536, lat: 41.8707727}, infoText: 'Marker1'},
        {position: {lng: -87.6638527, lat: 41.8708416}, infoText: 'Marker1'},
        {position: {lng: -87.6638519, lat: 41.8709847}, infoText: 'Marker1'},
        {position: {lng: -87.6638506, lat: 41.8710445}, infoText: 'Marker1'},
        {position: {lng: -87.6638446, lat: 41.8699563}, infoText: 'Marker1'},
        {position: {lng: -87.6638443, lat: 41.8698501}, infoText: 'Marker1'},
        {position: {lng: -87.6638418, lat: 41.8688549}, infoText: 'Marker1'},
        {position: {lng: -87.6638406, lat: 41.8707093}, infoText: 'Marker1'},
        {position: {lng: -87.6638397, lat: 41.8711199}, infoText: 'Marker1'},
        {position: {lng: -87.663834, lat: 41.8700229}, infoText: 'Marker1'},
        {position: {lng: -87.6638257, lat: 41.8706341}, infoText: 'Marker1'},
        {position: {lng: -87.6638096, lat: 41.8703632}, infoText: 'Markert1'}
      ]
    }
  },
  methods: {
          toggleInfoWindow: function(marker, idx) {
            // Custom marker:
            // https://developers.google.com/maps/documentation/javascript/examples/marker-symbol-custom
            this.infoWindowPos = marker.position;
            this.infoOptions.content = marker.infoText;

            //check if its the same marker that was selected if yes toggle
            if (this.currentMidx == idx) {
              this.infoWinOpen = !this.infoWinOpen;
            }
            //if different marker set infowindow to open and reset current marker index
            else {
              this.infoWinOpen = true;
              this.currentMidx = idx;

            }
          }

        }
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