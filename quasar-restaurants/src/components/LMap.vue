<template>
  <div>
    <div id="mapContainer" />
  </div>
</template>

<script>
import { defineComponent, onMounted, onBeforeMount } from 'vue'
import 'leaflet/dist/leaflet.css'
import L from 'leaflet'

export default defineComponent({
  name: 'LMap',

  props: {
    markers: {
      type: Array,
      required: false,
      default: () => []
    }
  },

  setup (props) {
    let map = null

    onMounted(() => {
      console.log(props.markers.value)
      createMapLayer()
    })

    onBeforeMount(() => {
      if (map) {
        map.remove()
      }
    })

    const createMapLayer = () => {
      map = L.map('mapContainer').setView([-9.387069399603352, -40.49908147926051], 14.4)
      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(map)

      if (props.markers.length > 0) {
        setMarkers()
      }
    }

    const setMarkers = () => {
      props.markers.map((marker) => {
        return L.marker([marker.latitude, marker.longitude]).addTo(map)
          .bindPopup(marker.descricao)
      })
    }
  }
})
</script>

<style scoped>
  #mapContainer {
    width: 100vw;
    height: calc(100vh - 50px);
  }
</style>
