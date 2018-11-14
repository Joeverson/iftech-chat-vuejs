<template>
  <div id="app">
    <section class="hero is-fullheight">
      <div class="hero-body">
        <messages :data='messages' />
      </div>
      <div class="hero-foot">        
        <send-message @send-message='updateMessage'/>          
      </div>
    </section>    
  </div>
</template>

<script>
import SendMessage from './components/SendMessage.vue'
import Messages from './components/Messages.vue'

export default {
  name: 'app',
  components: {
    Messages,
    SendMessage
  },
  data() {
    return {
      messages: []
    }
  },
  methods: {
    updateMessage(message) {
      // eslint-disable-next-line
      console.log(this.messages, message);
      
      this.messages.push(message);
    }
  }
}
</script>
