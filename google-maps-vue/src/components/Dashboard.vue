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
    :icon="customIcon"
    :draggable="true"
    :visible="m.visible == selected && m.price < maximum"
    @click="toggleInfoWindow(m,index)"
  />
</GmapMap>
<select v-model="selected">
  <option v-for="option in options" v-bind:key="option.text" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>Selected: {{ selected }}</span>
<input v-model="minimum" placeholder="0">
<p>Price min: {{ minimum }}</p>
<input v-model="maximum" placeholder="1500">
<p>Price max: {{ maximum }}</p>
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
      customIcon: {
        path: 'M 10, 20 a 10,10 0 1,1 20,0 a 10,10 0 1,1 -20,0',
        fillColor: 'green',
        fillOpacity: 0.8,
        scale: 1,
        strokeColor: 'black',
        strokeWeight: 2
      },
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
      minimum: 0,
      maximum: 1500,
      markers: [
        {position: {lng: -87.6649857, lat: 41.8690738}, icon: {
        path: 'M 125,5 155,90 245,90 175,145 200,230 125,180 50,230 75,145 5,90 95,90 z',
        fillColor: 'yellow',
        fillOpacity: 0.8,
        scale: 1,
        strokeColor: 'gold',
        strokeWeight: 14
      }, infoText: 'Marker 1', visible: 'B', price: 100},
        {position: {lng: -87.6648952, lat: 41.8690754}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6648825, lat: 41.8694949}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.664821, lat: 41.873856}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6648002, lat: 41.8690782}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6647942, lat: 41.8694922}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6647903, lat: 41.8718445}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6647069, lat: 41.8694913}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6647032, lat: 41.8690806}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6646183, lat: 41.8690946}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6645272, lat: 41.8690723}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.664521, lat: 41.8723198}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6645206, lat: 41.8719059}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6645124, lat: 41.8722341}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.66448, lat: 41.872642}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6644757, lat: 41.872697}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6644596, lat: 41.87249}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6644326, lat: 41.8690798}, icon: this.goldStar, infoText: 'Marker1', visible: 'A', price: 100},
        {position: {lng: -87.6644178, lat: 41.8719134}, icon: this.goldStar, infoText: 'Marker1', visible: 'B', price: 100},
        {position: {lng: -87.6643425, lat: 41.8690971}, icon: this.goldStar, infoText: 'Marker1', visible: 'B', price: 100},
        {position: {lng: -87.6643289, lat: 41.8719093}, icon: this.goldStar, infoText: 'Marker1', visible: 'B', price: 100},
        {position: {lng: -87.6642436, lat: 41.8695487}, icon: this.goldStar, infoText: 'Marker1', visible: 'B', price: 100},
        {position: {lng: -87.6642419, lat: 41.8690612}, icon: this.goldStar, infoText: 'Marker1', visible: 'B', price: 100},
        {position: {lng: -87.663973, lat: 41.8726416}, icon: this.goldStar, infoText: 'Marker1', visible: 'B', price: 100},
        {position: {lng: -87.6639715, lat: 41.8722495}, icon: this.goldStar, infoText: 'Marker1', visible: 'B', price: 100},
        {position: {lng: -87.6639605, lat: 41.871905}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6639305, lat: 41.873117}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.663926, lat: 41.8694948}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6639011, lat: 41.8691054}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.663886, lat: 41.8697116}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638559, lat: 41.8709124}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638536, lat: 41.8707727}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638527, lat: 41.8708416}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638519, lat: 41.8709847}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638506, lat: 41.8710445}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638446, lat: 41.8699563}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638443, lat: 41.8698501}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638418, lat: 41.8688549}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638406, lat: 41.8707093}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638397, lat: 41.8711199}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.663834, lat: 41.8700229}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638257, lat: 41.8706341}, icon: this.goldStar, infoText: 'Marker1', visible: 'C', price: 100},
        {position: {lng: -87.6638096, lat: 41.8703632}, icon: this.goldStar, infoText: 'Markert1', visible: 'C', price: 50} 
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