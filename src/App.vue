<template>
  <div id="app">
    <todos></todos>
  </div>
</template>

<script>
import Todos from './components/Todos'

export default {
  name: 'App',
  components: {
    Todos
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');
#app{
  max-width: 80vw;
  margin: 0 auto;
  font-family: 'Poppins', sans-serif;
}
</style>
