<template>
  <div id="app">
    <questionsEdit></questionsEdit>
  </div>
</template>

<script>
import questionsEdit from './components/questionsEdit'

export default {
  name: 'App',
  components: {
    questionsEdit
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
