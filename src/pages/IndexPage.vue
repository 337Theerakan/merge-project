<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
    <q-input
        filled
        v-model="id"
        label="Your id *"
        hint="id code"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please your id code']"
      />


      <q-input
        filled
        v-model="name"
        label="Your name *"
        hint="Name"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type your name']"
      />

      <q-input
        filled
        v-model="surename"
        label="Your surename*"
        hint="surename"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type surname']"
      />

      <q-input
        filled
        v-model="languge"
        label="ภาษา"
        hint="ภาษา"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'กรุณาใส่ภาษา พรีสส']"
      />


      <q-input
        filled
        type="number"
        v-model="age"
        label="Your age *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your age',
          val => val > 0 && val < 100 || 'Please type a real age'
        ]"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>

<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()
    const languge = ref("ภาษา")
    const id = ref("14")
    const name = ref("Theerakan")
    const surename = ref("kan")
    const age = ref(null)
    const accept = ref(false)

    return {
      name,
      surename,
      languge,
      age,
      id,
      accept,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            message: 'You need to accept the license and terms first'
          })
        }
        else {
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
        }
      },

      onReset () {
        id.value = null
        name.value = null
        surename.value = null
        age.value = null
        languge.value = null
        accept.value = false
      }
    }
  }
}
</script>
