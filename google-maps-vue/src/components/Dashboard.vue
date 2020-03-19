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
    :icon="getCustomIcon(m.price)"
    :draggable="true"
    :visible="isVisible(m)"
    @click="toggleInfoWindow(m,index)"
  />
</GmapMap>
<!-- all of these should be componentized -->
<input v-model="minimum" placeholder="0">
<p>Price min: {{ minimum }}</p>
<input v-model="maximum" placeholder="1500">
<p>Price max: {{ maximum }}</p>
<span>ZIP Code: </span>
<select v-model="zipCodeSelected">
  <option v-for="option in zipOptions" v-bind:key="option.text" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<select v-model="classDescriptionSelected">
  <option v-for="option in classDescriptionOptions" v-bind:key="option.text" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
<span>OVACLS: </span>
<select v-model="ovaClsSelected">
  <option v-for="option in ovaClsOptions" v-bind:key="option.text" v-bind:value="option.value">
    {{ option.text }}
  </option>
</select>
</div>
</template>

<script>
export default {
  name: 'Dashboard',
  props: {
    msg: String
  },
  // https://stackoverflow.com/questions/13488957/interpolate-from-one-color-to-another
  // https://stackoverflow.com/questions/5623838/rgb-to-hex-and-hex-to-rgb
  // https://campushippo.com/lessons/how-to-convert-rgb-colors-to-hexadecimal-with-javascript-78219fdb
  data: function () {
    return {
      zipCodeSelected: 60607,
      zipOptions: [
        {text: 60607, value: 60607},
        {text: 60608, value: 60608},
        {text: 60612, value: 60612},
        {text: 60614, value: 60614},
        {text: 60616, value: 60616},
        {text: 60618, value: 60618},
        {text: 60622, value: 60622}
      ],
      ovaClsSelected: 211,
      ovaClsOptions: [
        {text: 211, value: 211},
        {text: 212, value: 212},
        {text: 315, value: 315},
        {text: 314, value: 314},
        {text: 225, value: 225},
        {text: 297, value: 297},
        {text: 313, value: 313},
        {text: 318, value: 318},
        {text: 391, value: 391},
        {text: 396, value: 396},
        {text: 913, value: 913},
        {text: 915, value: 915},
        {text: 991, value: 991},
        {text: 996, value: 996}
      ],
      classDescriptionSelected: '2 or 3 story bldng, 7 or more units, sngle devel., 1 or more contig. parcels, in common ownership',
      classDescriptionOptions: [
        {text: '2 or 3 story bldng, 7 or more units, sngle devel., 1 or more contig. parcels, in common ownership', value: '2 or 3 story bldng, 7 or more units, sngle devel., 1 or more contig. parcels, in common ownership'},
        {text: '2 or 3 story non-frprf corridor apts, or california type apts, interior entrance', value: '2 or 3 story non-frprf corridor apts, or california type apts, interior entrance'},
        {text: 'Apartment buildings over three stories', value: 'Apartment buildings over three stories'},
        {text: 'Mixed commercial/residential building, 6 units or less, sq ft less than 20,000 ', value: 'Mixed commercial/residential building, 6 units or less, sq ft less than 20,000'},
        {text: 'Mixed use commercial/residential with apts. above seven units or more or building sq. ft. over 20,000', value: 'Mixed use commercial/residential with apts. above seven units or more or building sq. ft. over 20,000'},
        {text: 'Qualified single room occupancy improvements (must have cdu of sr)', value: 'Qualified single room occupancy improvements (must have cdu of sr)'},
        {text: 'Rental mdrn row houses, 7 or more unts in a sing. dvlpment or 1 or more contig. prcls in comm. ownrshp', value: 'Rental mdrn row houses, 7 or more unts in a sing. dvlpment or 1 or more contig. prcls in comm. ownrshp'},
        {text: 'Special residential improvements', value: 'Special residential improvements'},
        {text: 'Two or three story non-fireproof corridor apartments,or california type apartments, interior entrance', value: 'Two or three story non-fireproof corridor apartments,or california type apartments, interior entrance'},
        {text: 'Two or three story non-frprf. crt. and corridor apts or california type apts, no corridors, ex. entrance', value: 'Two or three story non-frprf. crt. and corridor apts or california type apts, no corridors, ex. entrance'},
        {text: 'Two to Six Apartments, Over 62 Years', value: 'Two to Six Apartments, Over 62 Years'}
      ],
      infoWindowPos: null,
      infoWinOpen: false,
      currentMidx: null,
      infoOptions: {
        content: '',
        pixelOffset: {
          width: 0,
          height: -35
        }
      },
      minimum: 0,
      maximum: 1500,
      markers: [
        {position: {lng: -87.6649857, lat: 41.8690738}, infoText: 'Marker 1', ZIP: 60608, classDescription: 'Two to Six Apartments, Over 62 Years', price: 20, ovaCls: 211},
        {position: {lng: -87.6648952, lat: 41.8690754}, infoText: 'Marker1', ZIP: 60607, classDescription: 'Two to Six Apartments, Over 62 Years', price: 100, ovaCls: 212},
        {position: {lng: -87.6648825, lat: 41.8694949}, infoText: 'Marker1', ZIP: 60612, classDescription: 'Two to Six Apartments, Over 62 Years', price: 100, ovaCls: 315},
        {position: {lng: -87.664821, lat: 41.873856}, infoText: 'Marker1', ZIP: 60614, classDescription: 'Two to Six Apartments, Over 62 Years', price: 100, ovaCls: 314}
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
          }, 
          getCustomIcon: function(price) {
            let fillColor = this.getLinearInterpOfColor(price/200)
            return {
              path: 'M 10, 20 a 10,10 0 1,1 20,0 a 10,10 0 1,1 -20,0',
              fillColor: fillColor,
              fillOpacity: 0.8,
              scale: 1,
              strokeColor: 'black',
              strokeWeight: 2
            }
          },
          getLinearInterpOfColor: function(fraction) {
            const rRed = 255;
            const gRed = 0;
            //const bRed = 0;

            const rGreen = 0;
            const gGreen = 255;
            //const bGreen = 0;

            const rNew = Math.round((rGreen - rRed) * fraction) + rRed;
            const gNew = Math.round((gGreen - gRed) * fraction) + gRed;
            const bNew = 0;

            console.log(rNew);

            return this.rgbToHex(rNew, gNew, bNew);
          },
          componentToHex: function(c) {
            var hex = Number(c).toString(16);
            if (hex.length < 2) {
                hex = "0" + hex;
            }
            return hex;
          },
          rgbToHex: function(r, g, b) {
            let hex = "#" + this.componentToHex(r) + this.componentToHex(g) + this.componentToHex(b);
            console.log(hex);
            return hex;
          },
          isVisible: function(marker) {
            let matchesPrice = marker.price <= this.maximum && marker.price >= this.minimum;
            let matchesZip = marker.ZIP == this.zipCodeSelected; 
            let matchesOvaCls = marker.ovaCls == this.ovaClsSelected;
            let matchesClassDescription = marker.classDescription == this.classDescriptionSelected
            return matchesPrice && matchesZip && matchesOvaCls && matchesClassDescription;
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