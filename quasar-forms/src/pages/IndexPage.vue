<template>
  <q-page class="container" padding>
    <h4>Formulário</h4>
    <!--<div class="row q-col-gutter-xs">-->
    <q-form @submit.prevent="onSubmit" class="row q-col-gutter-xs" ref="myForm">
      <q-input
        outlined
        v-model="form.nome"
        label="Nome"
        class="col-md-12 col-sm-12 col-xs-12"
        color="primary"
        :rules="[(val) => (val && val.length > 0) || 'Nome obrigatório']"
      >
        <template v-slot:prepend>
          <q-icon name="person"></q-icon>
        </template>
      </q-input>

      <q-input
        outlined
        v-model.number="form.idade"
        type="number"
        label="Idade"
        class="col-md-12 col-sm-12 col-xs-12"
        color="primary"
        :rules="[
          (val) => (val !== null && val !== '') || 'Idade obrigatória',
          (val) => (val > 0 && val < 100) || 'Informe uma idade válida',
        ]"
      >
        <template v-slot:prepend>
          <q-icon name="person"></q-icon>
        </template>
      </q-input>

      <q-input
        outlined
        v-model="form.email"
        label="Email"
        class="col-md-12 col-sm-12 col-xs-12"
        color="primary"
        suffix="@gmail.com"
        loading="true"
        :rules="[(val) => (val && val.length > 0) || 'Email obrigatório']"
      >
        <template v-slot:prepend>
          <q-icon name="email"></q-icon>
        </template>
      </q-input>

      <q-input
        outlined
        v-model="form.telefone"
        label="Telefone"
        mask="(##) #####-####"
        unmasked-value
        class="col-md-12 col-sm-12 col-xs-12"
        color="primary"
        :rules="[
          (val) => (val && val.length > 0) || 'Telefone obrigatório',
          (val) => val.length === 11 || 'Informe um telefone válido',
        ]"
      >
        <template v-slot:prepend>
          <q-icon name="phone"></q-icon>
        </template>
      </q-input>

      <q-select
        outlined
        v-model="form.tipoConta"
        :options="optionsTipoConta"
        label="Tipo de Conta"
        class="col-md-12 col-sm-12 col-xs-12"
        emit-value
        map-options
        :rules="[
          (val) => (val && val.length > 0) || 'Tipo de Conta obrigatório',
        ]"
      />
      <span class="text-bold">Sexo: </span>
      <q-option-group
        v-model="form.sexo"
        :options="optionsSexo"
        color="primary"
        class="col-md-12 col-sm-12 col-xs-12"
      />

      <span class="text-bold q-mt-md">Possui alguma dificuldade? </span>
      <q-option-group
        :options="optionsDificuldades"
        type="checkbox"
        v-model="form.dificuldades"
        class="col-md-12 col-sm-12 col-xs-12"
        color="primary"
      />

      <q-toggle
        v-model="form.notificacoes"
        checked-icon="check"
        color="primary"
        label="Receber notificações"
        unchecked-icon="clear"
      />

      <div class="col-12">
        <q-btn
          type="submit"
          label="Cadastrar"
          color="primary"
          class="float-right"
        >
        </q-btn>
      </div>
    </q-form>
    <!--</div>-->
  </q-page>
</template>

<script>
import { useQuasar } from 'quasar'
export default {
  setup () {
    const $q = useQuasar()
    return {
      onSubmit () {
        $q.notify({
          message: 'Cadastro realizado com sucesso!',
          color: 'primary',
          icon: 'check'
        })
      }
    }
  },
  data () {
    return {
      form: {
        nome: '',
        idade: null,
        email: '',
        telefone: null,
        tipoConta: '',
        sexo: 'NI',
        dificuldades: [],
        notificacoes: false
      },
      optionsTipoConta: [
        {
          label: 'Pessoa Física',
          value: 'PF'
        },
        {
          label: 'Pessoa Jurídica',
          value: 'PJ'
        }
      ],
      optionsSexo: [
        {
          label: 'Não informado',
          value: 'NI'
        },
        {
          label: 'Masculino',
          value: 'M'
        },
        {
          label: 'Feminino',
          value: 'F'
        }
      ],
      optionsDificuldades: [
        {
          label: 'Motoras',
          value: 'M'
        },
        {
          label: 'Visuais',
          value: 'V'
        },
        {
          label: 'Respiratórias',
          value: 'R'
        }
      ]
    }
  },
  methods () {
    return {}
  }
}
</script>

<style></style>
