<template>
  <q-page padding>
    <q-table
      :rows="posts"
      :columns="columns"
      row-key="name"
    >
      <template v-slot:top>
        <span class="text-h5">Artigos</span>
        <q-space/>
        <q-btn icon="add" color="primary" label="Novo" :to="{ name: 'formPost' }"/>
      </template>

      <template v-slot:body-cell-actions="props">
        <q-td :props="props" class="q-gutter-sm">
          <q-btn
          icon="edit"
          color="primary"
          dense
          @click="handleEditPost(props.row.id)"
          >
          </q-btn>
          <q-btn
          icon="delete"
          color="negative"
          dense
          @click="handleDeletePost(props.row.id)"
          >
          </q-btn>
        </q-td>
      </template>
    </q-table>
  </q-page>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import postsService from 'src/services/posts'
import { useQuasar } from 'quasar'
import { useRouter } from 'vue-router'

export default defineComponent({
  name: 'IndexPage',
  setup () {
    const { list, remove } = postsService()
    const $q = useQuasar()
    const router = useRouter()

    const posts = ref([])
    const columns = [
      { name: 'id', label: 'Id', field: 'id', sortable: true, align: 'left' },
      { name: 'title', label: 'Título', field: 'title', sortable: true, align: 'left' },
      { name: 'author', label: 'Autor', field: 'author', sortable: true, align: 'left' },
      { name: 'actions', label: 'Ações', field: 'actions', align: 'right' }
    ]

    onMounted(() => {
      getPosts()
    })

    const getPosts = async () => {
      try {
        const data = await list()
        posts.value = data
      } catch (error) {
        console.log(error)
      }
    }

    const handleDeletePost = async (id) => {
      try {
        $q.dialog({
          title: 'Remover',
          message: 'Deseja deletar este post?',
          cancel: true,
          persistent: true
        }).onOk(async () => {
          await remove(id)
          await getPosts()
          $q.notify({
            message: 'Apagado com sucesso',
            icon: 'check',
            color: 'positive'
          })
        })
      } catch (error) {
        $q.notify({
          message: 'Erro ao apagar post',
          icon: 'times',
          color: 'negative'
        })
      }
    }

    const handleEditPost = (id) => {
      router.push({
        name: 'formPost', params: { id }
      })
    }

    return {
      posts,
      columns,
      handleDeletePost,
      handleEditPost
    }
  }
})
</script>
