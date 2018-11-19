<template>
  <div class='container'>
    <div class="columns">
      <div class='column'>
        <input class="input is-large" 
          v-model="user.name" 
          type="text" 
          name="" 
          id="user-name"
          @keyup.enter="login()"/>
      </div>
      <div class='column is-one-quarter'>
        <button class='button is-success is-large is-fullwidth' @click='login()' >Fazer login</button>
      </div>
    </div>
  </div>
</template>

<script>  
  export default {
    name: 'login',
    data() {
      return {
        user: {
          name: ''
        }
      };
    },
    methods: {
      /**
       * Método responsável para poder
       * enviar um comando para o componente
       * pai.
       */
      login() {
        this.$emit("login", Object.assign({}, this.user))
      }
    } 
  }
</script>
