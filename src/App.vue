<template>
  <div id="app">
    <h1>To-DO List</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>
    <ul>
      <li v-for="item in ToDoItems" :key="item.id">
        <to-do-item :label="item.label" :done="item.done" :id="item.id"></to-do-item>
      </li>
    </ul>
  </div>
</template>

<script>
import uniqueId from 'lodash.uniqueid';
import ToDoItem from './components/ToDoItem';
import ToDoForm from './components/ToDoForm';

export default {
  name: 'App',
  components: {
    ToDoItem,
    ToDoForm
  },
  methods: {
    addToDo(toDoLabel) {
      this.ToDoItems.push({id: uniqueId('todo-'), label: toDoLabel, done: false })
    },
  },
  data() {
    return {
      ToDoItems: []
    }
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
