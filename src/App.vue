<template>
  <div id="app">
    <header>Minhas Tarefas</header>
    <Task/>
  </div>
</template>

<script>
import Task from './components/Task.vue';

export default {
  name: 'App',
  components: {
    Task,
  }
}
</script>

<style scoped>
header{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 80px;
  font-size: 40px;
  color: #FFF;
}

</style>
