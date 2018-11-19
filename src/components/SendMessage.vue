<template>
  <div class='container'>
    <div class="columns">
      <div class='column'>
        <input class="input is-large" 
          @keyup.enter="send()" 
          v-model="message.text" 
          type="text" 
          name="" 
          id="send-message"/>
      </div>
      <div class='column is-one-fifth'>
        <button 
          class='button is-success is-large is-fullwidth'          
          @click='send()' >Enviar</button>
      </div>
    </div>
  </div>
</template>

<script>  
  export default {
    name: 'send-message',
    data() {
      return {
        message: {
          author: ''          
        }
      };
    },
    methods: {
      /**
       * Método responsável por enviar
       * a mensagem que foi digitada para
       * o componente pai.
       */
      send() {
        this.$emit("send-message", Object.assign({}, this.message))
        this.clear()
      },
      /**
       * Método responsável por limpar
       * o campo de text quando finalizar 
       * o envio.
       */
      clear() {
        this.message.text = ''
      }
    }    
  }
</script>
