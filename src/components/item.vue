<template>
  <div :class="['todo-item', todo.completed ? 'completed' : '']">
    <input class="todo-check" type="checkbox" v-model="todo.completed">
    <label class="todo-text">{{todo.content}}</label>
    <button class="destroy" @click="deleteItem"></button>
  </div>
</template>

<script>
export default {
  name: 'todoList',
  props: {
    todo: {
      type: Object,
      require: true
    }
  },
  methods: {
    deleteItem () {
      this.$emit('delete', this.todo.id)
    }
  }
}
</script>

<style scoped>
  .todo-item{
    position: relative;
    background-color: #fff;
    border-bottom: 1px solid rgba(0, 0, 0, 0.3);
    font-size: 24px;
    line-height: 60px;
  }
  .todo-item.completed{
    color: #888;
    text-decoration: line-through;
  }
  .todo-item:hover .destroy::after{
    content: 'x';
  }
  .todo-check{
    width: 30px;
    height: 30px;
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto 0;
    margin-left: 20px;
    border: 1px solid rgba(0, 0, 0, 0.3);
    border-radius: 50%;
    outline: none;
    appearance: none;
  }
  .todo-check:checked{
    height: 1px;
  }
  .todo-text{
    margin-left: 70px;
  }
  .destroy{
    position: absolute;
    top: 0;
    right: 10px;
    margin: auto 0;
    width: 60px;
    height: 60px;
    font-size: 30px;
    color: palevioletred;
    border: none;
    background-color: transparent;
    cursor: pointer;
    transition: all .2s ease-out;
  }
</style>
