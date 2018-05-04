<template>
  <div class="tabs-wrap">
    <span>{{unFinishedTodoLength}}个任务未完成</span>
    <span class="tabs">
      <span :class="['tabs-item' , filter === state ? 'actived' : '']" v-for="(state,index) of states" :key="index" @click="toggleFilter(state)">{{state}}</span>
    </span>
    <span class="clear" @click="clearAllCompleted">清除已完成任务</span>
  </div>
</template>

<script>
export default {
  props: {
    filter: {
      type: String,
      require: true
    },
    todos: {
      type: Array,
      require: true
    }
  },
  data () {
    return {
      states: ['全部', '未完成', '完成']
    }
  },
  computed: {
    unFinishedTodoLength () {
      return this.todos.filter(todo => !todo.completed).length
    }
  },
  methods: {
    toggleFilter (state) {
      this.$emit('toggle', state)
    },
    clearAllCompleted () {
      this.$emit('clearAllCompleted')
    }
  }
}
</script>

<style scoped>
  .tabs-wrap{
    display: flex;
    justify-content: space-between;
    line-height: 30px;
    padding:6px;
    background-color: #fff;
    font-size: 14px;
  }
  .tabs{
    width: 200px;
    display: flex;
    justify-content: space-around;
  }
  .tabs-item{
    padding: 0 10px;
    border: 1px solid rgba(201, 3, 3, 0);
    border-radius: 5px;
    cursor: pointer;
  }
  .tabs-item.actived{
    border-color: rgb(65, 184, 131, .4);;
  }
  .clear{
    cursor: pointer;
  }

</style>
