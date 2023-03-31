<template>
  <TableEl msg="这是一个表单控件"/>
</template>

<script>
import TableEl from './components/table/TableEl.vue'

export default {
  name: 'App',
  components: {
    TableEl
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
