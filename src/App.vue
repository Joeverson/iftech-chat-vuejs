<template>
  <div id="app">
    <section class="hero is-fullheight">
      <div class="hero-body">
        <messages 
          :data='messages' />
      </div>
      <div class="hero-foot">        
        <send-message 
          v-if='isUserRegistred' 
          @send-message='updateMessage'/>          
        <Login 
          v-else
          :user='user'
          @login='login' />
      </div>
    </section>    
  </div>
</template>

<script>
import io from 'socket.io-client';
import SendMessage from './components/SendMessage.vue'
import Login from './components/Login.vue'
import Messages from './components/Messages.vue'

const URI_SOCKET = 'http://localhost:5000'

export default {
  name: 'app',
  components: {
    Messages,
    SendMessage,
    Login
  },
  data() {
    return {
      socket: io(URI_SOCKET),
      messages: [],
      user: {
        name: null
      }
    }
  },
  computed: {
    isUserRegistred() {
      return this.user.name !== null
    }
  },
  mounted() {
    this.socket.on('listen', (messages) => {
      const messagesSide = messages.map(message => {
        if (messages.author === this.user.name) {
          messages.side = 'me'
        } else {
          messages.side = 'other'
        }
        return message
      });

      this.messages = this.messages.concat(messagesSide)
    })
  },
  methods: {
    updateMessage(message) {
      message.author = this.user.name

      this.socket.emit('speak', message)      
    },
    login(user) {
      this.user = Object.assign(this.user, user)
    }
  }
}
</script>
