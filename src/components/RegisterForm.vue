<template>
  <modal title="Register Form"
  @close = "$emit('close')">
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <div class="form-item" :class ="{errorInput: $v.login.$error}">
          <label>Login</label>
          <p class = "errorText" v-if="!$v.login.required">Login is required</p>
          <p class = "errorText" v-if="!$v.login.minLength">Login must have at least {{ $v.login.$params.minLength.min }}!</p>
          <input v-model="login" 
          :class='{error: $v.login.$error}'
          @change="$v.login.$touch()">
        </div>
        <div class="form-item" :class ="{errorInput: $v.email.$error}">
          <label>E-mail</label>
          <p class = "errorText" v-if="!$v.email.required">Email is required</p>
          <p class = "errorText" v-if="!$v.email.email">Email is not correct</p>
          <input v-model="email" 
          :class='{error: $v.email.$error}'
          @change="$v.email.$touch()">
        </div>
        <div class="form-item" :class ="{errorInput: $v.password.$error}">
          <label>Password</label>
          <p class = "errorText" v-if="!$v.password.required">Password is required</p>
          <p class = "errorText" v-if="!$v.password.minLength">Password must have at least {{ $v.password.$params.minLength.min }}!</p>
          <input type="password" v-model="password" 
          :class='{error: $v.password.$error}'
          @change="$v.password.$touch()">
        </div>
        <div class="form-item" :class ="{errorInput: $v.repeatPassword.$error}">
          <label>Repeat Password</label>
          <p class = "errorText" v-if="!$v.repeatPassword.sameAsPassword">Passwords not same</p>
          <input type="password" v-model="repeatPassword" 
          :class='{error: $v.repeatPassword.$error}'
          @change="$v.repeatPassword.$touch()">
        </div>

        <button class = "btn btnPrimary">Submit</button>
      </form>
    </div>
  </modal>  
</template>

<script>
import modal from '@/components/UI/Modal.vue'
import { required, minLength, email, sameAs  } from "vuelidate/lib/validators";

export default {
  components: {
    modal
  },
  data () {
    return {
      login: '',
      email: '',
      password: '',
      repeatPassword: '',
    }
  },
  validations: {
    login: {
      required,
      minLength: minLength(6)
    },
    email: {
      required,
      email
    },
    password: {
      required,
      minLength: minLength(6)
    },
    repeatPassword: {
      sameAsPassword: sameAs('password')
    }
  },
  methods: {
    onSubmit () {
      this.$v.$touch()
      if (!this.$v.$invalid) {
          const user = {
            login: this.login,
            email: this.email,
            password: this.password
          }
            console.log(user);
            this.resetData();
            this.$v.$reset()
            this.$emit('close')
      }
    },
    resetData () {
    this.login = ''
    this.email = ''
    this.password = ''
    this.repeatPassword = ''
    }
  }

}
</script>

<style>

</style>