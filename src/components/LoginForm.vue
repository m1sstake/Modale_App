<template>
  <modal title="Login Form"
  @close = "$emit('close')">
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <label>Login</label>
        <input maxlength="30" v-model = "login">
        <label>Password</label>
        <input type="password" v-model = "password">
        <button class = "btn btnPrimary">Submit</button>
      </form>
        <div class = "footer">
          <p style="cursor:pointer; color:blue;" v-on:click = "redirectToRegisterForm">Register</p>
        </div>
    </div>
  </modal>
</template>

<script>
import modal from "@/components/UI/Modal.vue"

export default {
  components: {
    modal
  }, 
  data () {
    return {
      login: '',
      password: ''
    }
  },
  methods: {
    onSubmit () {

      if (this.login == '' || this.password == '') {
        return false;
      }
      else {
      const user = {
        login: this.login,
        password: this.password
      }
      console.log(user);
      this.$emit('close')
      }
    },
    redirectToRegisterForm () {
      this.$emit('close')
      this.$emit('showRegisterForm')
    }
  }
}
</script>

<style lang = "scss">
.footer {
  background-color: #f2f3f5;
  padding: 7px;
  margin-top:25px;
}

</style>