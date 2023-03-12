<template>
  <q-page>
    <l-map
      v-if="!loading"
      :markers="markers"
    />
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import LMap from 'src/components/LMap.vue'
import { api } from 'boot/axios'

export default defineComponent({
  name: 'MapPage',
  components: { LMap },
  setup () {
    const markers = ref([])
    const loading = ref(true)

    onMounted(() => {
      handleGetList()
    })

    const handleGetList = async () => {
      try {
        loading.value = true
        const { data } = await api.get('restaurants')
        markers.value = data.data.map((restaurant) => {
          return {
            uid: restaurant.uid,
            ...restaurant.attributes
          }
        })
        loading.value = false
      } catch (error) {
        loading.value = false
        console.error(error)
      }
    }

    return {
      markers,
      loading
    }
  }
})
</script>
