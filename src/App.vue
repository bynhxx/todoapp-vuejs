<template>
  <div id="app">
    <header>My tasks</header>

    <Task/>
  </div>
</template>

<script>

import Task from './components/Task'
export default {
  name: 'App',
  components: {
    Task
  }
}
</script>

<style scoped>
  header{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 80px;
    font-size: 35px;
    text-transform: uppercase;
    font-weight: bold;
    letter-spacing: -2px;
  }
</style>
