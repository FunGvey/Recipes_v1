<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Recipes App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/Main.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
