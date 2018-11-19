<template>
  <div class='container'>
    <div>
      <ul id='messages'>        
        <li 
          v-for="(message, i) in data" 
          v-bind:key="i" 
          :class="message.side">
          <small class='my-name is-outlined'>{{ message.author }} - {{ message.created_at }}</small> 
          <br>
          <span>{{ message.text }}</span>
        </li>      
      </ul>
    </div>    
  </div>
</template>

<script>
export default {
  name: "messages",
  props: {
    data: Array
  },
  /**
   * Quando atualiza ele joga o scroll 
   * para o o fim, com isso mostrando
   * as ultimas mensagens.
   */
  updated() {
    var scrollingElement = (document.scrollingElement || document.body)
    scrollingElement.scrollTop = scrollingElement.scrollHeight
  }
};
</script>

<style>
.my-name {
  color: #808080;
  font-style: italic;
  font-size: 11px;
}
.others {
  text-align: right;
}
.me {
  text-align: left;
}
</style>
