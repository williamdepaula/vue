<script>
  import { required, sameAs, email } from 'vuelidate/lib/validators'

  export default {
      mounted () {
        this.$bus.$on('navigate', this.reset);
      },
      validations: {
          user: {
              required
          },
          password: {
              required
          },
          password2: {
              sameAsPassword: sameAs('password')
          },
          emailValue: {
              required,
              email
          }
      },
      data () {
          return {
              user: '',
              password: '',
              password2: '',
              emailValue: ''
          }
      },
      methods: {
          reset (selected) {
               if( selected === 'signin') {
                 this.user = ''
                 this.password = ''
                 this.password2 = ''
                 this.emailValue = ''
                   this.$v.$reset()
             }
          },
          submit () {
              if (!this.$v.$invalid) {
                  this.$emit('do-sign-up', {...this.$data});
              } else {
                  this.$v.$touch();
              }
          }
      }
  }
</script>

<template>
  <form action="#" @submit.prevent="submit" class="sign-up-htm">
    <div class="group">
      <label
        for="user"
        :class="{ invalid: $v.user.$dirty && $v.user.$invalid }"
        class="label">Login</label>
      <input
        id="user"
        type="text"
        class="input"
        :class="{ invalid: $v.user.$dirty && $v.user.$invalid }"
        @input="$v.user.$touch()"
        v-model="user">
    </div>
    <div class="group">
      <label
        for="sign-up-pass"
        :class="{ invalid: $v.password.$dirty && $v.password.$invalid }"
        class="label">Senha</label>
      <input
        id="sign-up-pass"
        v-model="password"
        type="password"
        class="input"
        :class="{ invalid: $v.password.$dirty && $v.password.$invalid }"
        @input="$v.password.$touch()"
        data-type="password">
    </div>
    <div class="group">
      <label
        for="sign-up-pass2"
        :class="{ invalid: $v.password2.$dirty && $v.password2.$invalid }"
        class="label">Resetar Senha</label>
      <input
        id="sign-up-pass2"
        v-model="password2"
        :class="{ invalid: $v.password2.$dirty && $v.password2.$invalid }"
        @input="$v.password2.$touch()"
        type="password"
        class="input"
        data-type="password">
    </div>
    <div class="group">
      <label
        for="email"
        :class="{ invalid: $v.emailValue.$dirty && $v.emailValue.$invalid }"
        class="label">Endereço de Email</label>
      <input
        id="email"
        type="text"
        v-model="emailValue"
        :class="{ invalid: $v.emailValue.$dirty && $v.emailValue.$invalid }"
        @input="$v.emailValue.$touch()"
        class="input">
    </div>
    <div class="group">
      <input type="submit" class="button" value="Inscrever-se">
    </div>
    <div class="hr"></div>
  </form>
</template>

