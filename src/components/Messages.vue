<template>
  <div class='container' id="screen">
    <div class="screen">
      <ul>
        <li v-for="(message, i) in data" v-bind:key="i" :class="message.side">
          <small class='my-name is-outlined'>{{ message.author }}</small> 
          <br>
          <span>{{ message.text }}</span>
        </li>      
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'messages',
    props: {
      data: Array
    },
    updated() {      
      this.$el.scrollTop = this.$el.scrollHeight;
    }
  }
</script>

<style>
  .screen {
    max-height: 500px;
    overflow-y: scroll;
  }
  .my-name {
    color: #808080
  }
  .others{
    text-align: right
  }
  .me{
    text-align: left
  }
</style>
