<template>
   <div class="q-pa-md row q-gutter-md">
    <q-card
    v-for="card in cards" :key="card"
    style="max-width: 300px; width: 210px">
      <q-skeleton height="200px" square />

      <q-item>
        <q-item-section>
          <q-item-label>
            <q-skeleton animation="pulse-y" class="q-mt-md" type="rect" />
          </q-item-label>
          <q-item-label>
            <q-skeleton animation="pulse-y" class="q-mt-sm" type="QBadge" />
          </q-item-label>
          <q-item-label caption>
            <q-skeleton animation="pulse-y" class="q-mt-md" type="text" />
          </q-item-label>
          <q-item-label caption>
            <q-skeleton animation="pulse-y" type="text" />
          </q-item-label>
          <q-item-label caption>
            <q-skeleton animation="pulse-y" type="text" />
          </q-item-label>
        </q-item-section>
      </q-item>

    </q-card>
  </div>
</template>

<script>
export default {
  name: 'SkeletonCard',
  props: {
    cards: {
      type: Number,
      default: 4,
      required: false
    }
  }
}
</script>
