<template>
  <div id="app">
    <div class="cover"></div>
    <todo-header/>
    <todo-list/>
    <todo-footer/>
  </div>
</template>

<script>
import todoHeader from './components/header'
import todoFooter from './components/footer'
import todoList from './components/todo'

export default {
  components: {
    todoHeader,
    todoFooter,
    todoList
  }
}
</script>

<style>
  body{
    background-image: url(./assets/unsplash.jpg);
    background-size: cover;
    background-repeat: no-repeat;
  }

  .cover{
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: #555;
    opacity: 0.5;
    z-index: -1;
  }

</style>
