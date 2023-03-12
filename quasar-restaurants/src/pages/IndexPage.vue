<template>
  <q-page padding>
    <div class="q-pa-md">
      <q-table
          color="primary"
          card-class="bg-blue-7 text-blue-2"
          table-class="text-blue-1"
          table-header-class="text-blue-3"
          flat
          bordered
          title="Restaurantes"
          :rows="restaurants"
          :columns="columns"
          row-key="uid"
          :loading="loading"
        >
        <template v-slot:top-right>
          <q-btn text-color="primary"
            color="white"
            label="Novo"
            icon="add"
            :to="{ name: 'form' }"
          >
          </q-btn>
        </template>

        <template v-slot:body-cell-acoes="props">
          <q-td>
            <q-btn
              @click="handleDelete(props.row.uid)"
              color="red-5"
              dense
              icon="delete"
              class="no-shadow"
            />
          </q-td>

        </template>
      </q-table>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import { api } from 'boot/axios'
import { useQuasar } from 'quasar'

const columns = [
  {
    name: 'uid',
    label: 'ID',
    align: 'left',
    field: row => row.uid,
    sortable: true
  },
  {
    name: 'descricao',
    label: 'Descrição',
    align: 'left',
    field: row => row.descricao,
    sortable: true
  },
  {
    name: 'latitude',
    label: 'Latitude',
    align: 'left',
    field: row => row.latitude,
    sortable: true
  },
  {
    name: 'longitude',
    label: 'Longitude',
    align: 'left',
    field: row => row.longitude,
    sortable: true
  },
  {
    name: 'acoes',
    label: 'Ações',
    align: 'left',
    field: row => row.acoes,
    sortable: true
  }
]

export default defineComponent({
  name: 'IndexPage',

  setup () {
    const $q = useQuasar()
    const restaurants = ref([])
    const loading = ref(true)

    onMounted(() => {
      handleGetList()
    })

    const handleGetList = async () => {
      try {
        loading.value = true
        const { data } = await api.get('restaurants')
        restaurants.value = data.data.map((restaurant) => {
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

    const handleDelete = async (uid) => {
      try {
        $q.dialog({
          title: 'Remover',
          message: 'Você realmente deseja remover este restaurante da lista?',
          cancel: true,
          persistent: true
        }).onOk(async () => {
          await api.delete(`restaurants/${uid}`)
          await handleGetList()
          $q.notify({
            message: 'Removido com sucesso',
            icon: 'check',
            color: 'negative'
          })
        })
      } catch (error) {
        console.error(error)
      }
    }

    return {
      columns,
      restaurants,
      handleGetList,
      handleDelete,
      loading
    }
  }
})
</script>
