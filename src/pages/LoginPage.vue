<template>
  <div class="window-height window-width row justify-center centers items-center">
    <div style="width: 400px;">
      <q-form @submit="onSubmit">
        <q-input filled v-model="username" label="Usuario *" lazy-rules
          :rules="[val => val && val.length > 0 || 'Please type something']" />

        <q-input filled type="password" v-model="password" label="Contraseña *" lazy-rules :rules="[
          val => val !== null && val !== '' || 'Please type your password'
        ]" />

        <div>
          <q-btn label="Iniciar sesión" type="submit" color="primary" />
        </div>
      </q-form>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'LoginPage',
  setup() {
    const username = ref(null)
    const password = ref(null)

    return {
      username,
      password,

      onSubmit() {
        console.log('logged in')
      },
    }
  }
}
</script>
