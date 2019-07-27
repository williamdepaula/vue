<script>
  import SignIn from './sign-in'
  import SignUp from './sign-up'

  export default {
      components: {
          SignIn,
          SignUp
      },
      data () {
          return {
              navigation: 'signin'
          }
      },
      methods: {
          navigate () {
              this.$bus.$emit('navigate', this.navigation)
          },
          doSignIn(obj) {
              // Faz chamada AJAX
              console.log(obj);
          },
          doSignUp(obj) {
              // Faz chamada AJAX
              console.log(obj);
          }
      }
  }
</script>

<template>
  <div>
      <div class="login-wrap">
        <div class="login-html">

          <input
            id="tab-1"
            type="radio"
            name="tab"
            v-model="navigation"
            value="signin"
            @change="navigate"
            class="sign-in"
            checked>
          <label for="tab-1" class="tab">Entrar</label>

          <input
            id="tab-2"
            type="radio"
            name="tab"
            v-model="navigation"
            value="signup"
            @change="navigate"
            class="sign-up">
          <label for="tab-2" class="tab">Inscrever-Se</label>

          <div class="login-form">

            <sign-in @do-sign-in="doSignIn"/>

            <sign-up @do-sign-up="doSignUp"/>

          </div>
        </div>
      </div>
  </div>
</template>

<style src="./style.css">
</style>
