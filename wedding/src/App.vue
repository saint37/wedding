<template>
  <div id="app">
    <Wedding msg="Stupid Bread"/>
  </div>
</template>

<script>
import Wedding from './components/Wedding.vue'

export default {
  name: 'App',
  components: {
    Wedding
  }
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
