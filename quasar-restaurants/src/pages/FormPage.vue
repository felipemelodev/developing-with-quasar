<template>
  <q-page padding>
    <q-form class="row q-col-gutter-sm justify-center" @submit="handleSubmit">
      <q-input
        label="Descrição"
        outlined
        v-model="form.descricao"
        class="col-xs-12 col-sm-12 col-md-6 col-lg-5"
        :rules="requiredRule"
      />
      <q-input
        label="Latitude"
        outlined
        v-model="form.latitude"
        class="col-xs-12 col-sm-12 col-md-6 col-lg-5"
        :rules="requiredRule"
      />
      <q-input
        label="Longitude"
        outlined
        v-model="form.longitude"
        class="col-xs-12 col-sm-12 col-md-6 col-lg-5"
        :rules="requiredRule"
      />
      <div class="col-xs-12 col-sm-12 col-md-6 col-lg-5">
        <q-btn
          label="Salvar"
          color="primary"
          class="float-right q-mt-md"
          type="submit"
        />
        <q-btn
          label="Cancelar"
          color="white"
          text-color="primary"
          class="float-right q-mt-md q-mr-md"
          :to="{ name: 'home' }"
        />
      </div>
    </q-form>
  </q-page>
</template>

<script>
import { defineComponent, ref } from 'vue'
import { api } from 'boot/axios'
import { useRouter } from 'vue-router'
import { useQuasar } from 'quasar'

export default defineComponent({
  name: 'FormPage',

  setup () {
    const form = ref({
      descricao: '',
      latitude: '',
      longitude: ''
    })

    const $q = useQuasar()
    const router = useRouter()

    const requiredRule = [
      valor => (valor && valor.length > 0) || 'Campo obrigatório'
    ]

    const handleSubmit = async () => {
      try {
        await api.post('restaurants', form.value)
        router.push({ name: 'home' })
        $q.notify({
          message: 'Adicionado com sucesso',
          icon: 'check',
          color: 'positive'
        })
      } catch (error) {
        console.error(error)
      }
    }

    return {
      form,
      handleSubmit,
      requiredRule
    }
  }
})

</script>
