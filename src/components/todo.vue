<template>
  <div class="todo-wrap">
    <div >
      <input class="todo-input" type="text" placeholder="要干什么呢"  autofocus  @keyup.enter="addTodo"/>
      <!-- <button @click="addTodo">add</button> -->
    </div>
    <todo-item v-for="todo of filteredTodos" :todo="todo" :key="todo.id" @delete="deleteTodo"/>
    <todo-tabs :filter="filter" :todos="todos" @toggle="toggleFilter" @clearAllCompleted="clearAllCompleted"/>
  </div>
</template>

<script>
import todoItem from './item'
import todoTabs from './tabs'

let id = 0

export default {
  name: 'app',
  components: {
    todoItem,
    todoTabs
  },
  data () {
    return {
      todos: [],
      filter: '全部'
    }
  },
  computed: {
    filteredTodos () {
      if (this.filter === '全部') {
        return this.todos
      }
      const completed = this.filter === '完成'
      return this.todos.filter(todo => todo.completed === completed)
    }
  },
  methods: {
    addTodo (e) {
      if (e.target.value.trim()) {
        this.todos.unshift({
          id: id++,
          content: e.target.value.trim(),
          completed: false
        })
        e.target.value = ''
      }
    },
    deleteTodo (id) {
      this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
    },
    toggleFilter (state) {
      this.filter = state
    },
    clearAllCompleted () {
      this.todos = this.todos.filter(todo => todo.completed === false)
    }
  }
}
</script>

<style scoped>
  .todo-wrap{
    margin: 0 auto;
    width: 600px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
  }
  .todo-input{
    width: 100%;
    border: none;
    font-size: 24px;
    line-height: 2em;
    padding: 10px;
    padding-left:40px;
    box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.2);
    outline: none;
    box-sizing: border-box;
  }
</style>
