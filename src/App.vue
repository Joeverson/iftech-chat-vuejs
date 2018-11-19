<template>
  <div id="app">
    <nav class="navbar is-fixed-bottom" role="navigation" aria-label="main navigation">
      <div class="navbar-item">
        <send-message 
          v-if='isUserRegistred' 
          @send-message='updateMessage'
          />          
        <Login 
          v-else
          :user='user'
          @login='login' />
      </div>
    </nav>
    <section class="hero">
      <div class="hero-body">
        <messages 
          :data='messages' />
      </div>
    </section>   
  </div>
</template>

<script>
import io from "socket.io-client";
import moment from "moment";
import SendMessage from "./components/SendMessage.vue";
import Login from "./components/Login.vue";
import Messages from "./components/Messages.vue";

const URI_SOCKET = "http://localhost:5000";

export default {
  name: "app",
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
    };
  },
  computed: {
    isUserRegistred() {
      return this.user.name !== null;
    }
  },  
  mounted() {
    /**
     * Adicionando listener para ouvir 
     * tudo o que o socket.io estiver 
     * enviando.
     */
    this.socket.on("listen", messages => {
      /**
       * Organizando as mensagens que vem
       * do servidor de acordo com o tipo
       * de usuário que esta enviando
       */
      this.messages = messages.map(message => this.chooseSide(message));
    });
  },
  methods: {
    /**
     * Método responsável por atualizar a listagem de 
     * mensagens que o usuario envia, com isso mandando
     * para o servidor e depois registrando na tela.
     */
    updateMessage(message) {
      message.author = this.user.name;
      message.created_at = moment().format('DD/MM/YYYY HH:mm:ss')
      this.socket.emit("speak", message);
    },
    /**
     * Método responsável por fazer o login do 
     * usuário, no caso registrar o nome do usuário
     * e fazer o controle das mensagens com base
     * no nome do mesmo.
     */
    login(user) {
      this.user = Object.assign(this.user, user);
      this.user.name = `@${this.user.name}`
    },
    /**
     * Método responsável por colocar a mensagem
     * no lado esquerdo ou direito dependendo
     * de quem enviou a mensagem, caso seja a do
     * usuário logado é "me", caso não "other"
     */
    chooseSide(message) {     
      if (message.author === this.user.name) {
        message.side = "me";
      } else {
        message.side = "others";
      }
      return message;
    }
  }  
};
</script>
<style scoped>
  section{
    margin-bottom: 80px !important;
  }
</style>
