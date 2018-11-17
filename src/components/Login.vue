<template>
  <div class='container'>
    <div class="columns">
      <div class='column'>
        <input class="input is-large" v-model="user.name" type="text" name="" id="user-name"/>
      </div>
      <div class='column is-one-quarter'>
        <button class='button is-success is-rounded is-large is-fullwidth' @click='$emit("login", Object.assign({}, user))' >Fazer login</button>
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
    }    
  }
</script>
