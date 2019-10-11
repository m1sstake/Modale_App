<template>
<div class="wrapper">

  <div class="wrapper-content">
    <section>
      <div class="container">

        <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
        <!-- first modal -->
        <modals
        title="First modal"
        v-show="modalFirst"
        @close="modalFirst = false">
        
        <div slot="body">
          <p>Text text text</p>
          <button class = "btn btnPrimary" @click="modalFirst = !modalFirst">Well Done!</button>
        </div>

        </modals>

        <!-- modal second -->
        <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show modal with form</button>

        <modals
        title="Modal with form"
        v-show="modalSecond.show"
        @close="modalSecond.show = false">
        
        <div slot="body">
          <form @submit.prevent="submitSecondForm">
            <label>Name:</label>
            <input type="text" required v-model="modalSecond.name">
            <label>Email:</label>
            <input type="email" v-model="modalSecond.email">
            <button class = "btn btnPrimary">Submit</button>
          </form>
        </div>
        </modals>

        <!-- modalValidate -->

        <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show modal with form + validate</button>
        <modalValidate v-show ="modalValidate" @close = "modalValidate = false"/>

        <br><br>
        <!-- Login Form -->
        <button class="btn btnPrimary" @click="loginForm = true">Show modal with Login form</button>
        <loginForm v-show="loginForm" @close = "loginForm = false" @showRegisterForm = "registerForm = true"/>
        <registerForm v-show = "registerForm" @close= "registerForm = false"/>

      </div>
    </section>
  </div>
</div>
</template>

<script>
import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'
import loginForm from '@/components/LoginForm.vue'
import registerForm from '@/components/RegisterForm.vue'
export default {
  components: {
    modals,
    modalValidate,
    loginForm,
    registerForm
  },
  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: ''
      },
      modalValidate: false,
      loginForm: false,
      registerForm: false
    }
  },
  methods: {
    submitSecondForm () {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      })
      this.modalSecond.name = ''
      this.modalSecond.email = ''
      this.modalSecond.show = false
    },
  }
}
</script>
<style>

</style>
