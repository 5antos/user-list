<template>
  <div id="app">
    <UsersList/>
  </div>
</template>

<script>
  import UsersList from './components/UsersList.vue'

  export default {
    name: 'App',
    components: {
      UsersList
    }
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>