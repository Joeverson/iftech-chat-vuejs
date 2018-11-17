<template>
  <div class='container'>
    <div class="columns">
      <div class='column'>
        <input class="input is-large" v-model="message.text" type="text" name="" id="send-message"/>
      </div>
      <div class='column is-one-quarter'>
        <button class='button is-success is-rounded is-large is-fullwidth' @click='$emit("send-message", Object.assign({}, message))' >Enviar</button>
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
          author: '',
          who: '',
          text: ''
        }
      };
    }    
  }
</script>
