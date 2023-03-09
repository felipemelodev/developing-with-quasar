<template>
  <q-page class="q-pa-md">
    <skeleton-card
      v-if="load"
    />
    <div v-else class="col-12 row q-col-gutter-md">
      <div v-for="c in 4" :key="c" class="col-3">
        <q-card
        class="my-card">
          <img src="https://cdn.quasar.dev/img/mountains.jpg">
          <q-card-section>
            <div class="text-h6">Our Changing Planet</div>
            <div class="text-subtitle2">by John Doe</div>
          </q-card-section>
          <q-card-section class="q-pt-none">
            {{ lorem }}
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue'
import SkeletonCard from '../components/skeletons/SkeletonCard.vue'

export default defineComponent({
  name: 'CardPage',
  setup () {
    return {
      lorem: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.'
    }
  },
  components: {
    SkeletonCard
  },
  data () {
    return {
      load: true
    }
  },
  mounted () {
    setTimeout(() => {
      this.load = false
    }, 3000)
  }
})
</script>
