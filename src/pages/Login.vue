<template>
  <q-page class="bg-white window-width row justify-center items-center">
    <div class="column">
      <div class="row">
        <h5 class="text-h4 text-primary q-my-md" href="/">Genius</h5>
      </div>
      <div class="row">
        <q-card square bordered class="q-pa-lg shadow-1">
          <q-card-section>
            <q-form class="q-gutter-md">
              <q-input square filled clearable v-model="username" type="username" label="username" />
              <q-input square filled clearable v-model="password" type="password" label="password" />
            </q-form>
          </q-card-section>
          <q-card-actions class="q-px-md">
            <BaseButton unelevated  label="login" size="lg" class="full-width bg-primary" @click="login"></BaseButton>
          </q-card-actions>
          <q-card-section class="text-center q-pa-none">
            <p class="text-grey-6">Not reigistered? Created an Account</p>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>


<script>
// import Login02edaecc from 'app/src-cordova/platforms/android/app/build/intermediates/merged_assets/debug/out/www/assets/Login.02edaecc';
import { defineComponent, ref } from 'vue'

import { useUserStore } from '../stores/user/user'

export default defineComponent({
  name: 'Login',
  setup () {
    const userStore = useUserStore();
    return { userStore }

  },
  data() {
    return {
      username: "",
      password: "",
    }
  },
  methods: {
    async login() {
      try{
        await this.userStore.signIn(this.username, this.password);
        this.$router.push('/home')


      }
      catch(error){
        alert("500 Internal Server error");
        this.$router.push('/login')
      }

    }
  },


  
})
</script>

<style>
.q-card {
  width: 360px;
}

@media only screen and (max-width: 360px) {
  .q-card {
    width: 290px;
  }
}
</style>