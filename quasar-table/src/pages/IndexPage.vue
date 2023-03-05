<template>
  <q-page>
    <div class="row">
      <q-table
        title="Lorem Ipsum"
        :rows="rows"
        :columns="columns"
        row-key="id"
        separator="cell"
        class="col"

      >
      <template v-slot:body="props">
        <q-tr :props="props">
          <q-td auto-width>
            <q-btn size="sm" color="primary" round dense @click="props.expand = !props.expand" :icon="props.expand ? 'remove' : 'add'" />
          </q-td>
          <q-td
            v-for="col in props.cols"
            :key="col.name"
            :props="props"
          >
            {{ col.value }}
          </q-td>
        </q-tr>
        <q-tr v-show="props.expand" :props="props">
          <q-td colspan="100%">
            <div class="text-left">{{ props.row.body }}.</div>
          </q-td>
        </q-tr>
      </template>
      <!-- <template v-slot:body-cell-action="props">
        <q-td :props="props">
          <q-btn
            icon="create"
            color="primary"
            size="sm"
            @click="editPost(props.row)"
          />
          <q-btn
            icon="delete"
            color="negative"
            size="sm"
            class="q-ml-sm"
            @click="deletePost(props.row)"
          />
        </q-td>
      </template> -->
      </q-table>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'IndexPage',
  data () {
    return {
      columns: [
        {
          label: ''
        },
        {
          name: 'id',
          label: 'Id Post',
          field: 'id',
          align: 'left',
          sortable: true
        },
        {
          name: 'title',
          label: 'Title',
          field: 'title',
          align: 'left',
          sortable: true
        }
        /* {
          name: 'action',
          label: 'Action',
          align: 'right',
          sortable: true
        } */
      ],
      rows: [],
      selected: ref([])
    }
  },
  mounted () {
    this.getPosts()
  },
  methods: {
    getPosts () {
      this.$axios.get('https://jsonplaceholder.typicode.com/posts')
        .then((res) => {
          this.rows = res.data
        })
        .catch((err) => {
          console.log(err)
        })
    },
    editPost (idPost) {
      console.log(idPost)
    },
    deletePost (idPost) {
      console.log(idPost)
    }
  }
})
</script>
