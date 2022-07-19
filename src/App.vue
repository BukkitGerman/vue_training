<template>
  <div id="app">
    <h1>To-DO List</h1>
    <to-do-form @todo-added="addToDo"></to-do-form>
    <h2 id="list-summary">{{listSummary}}</h2>
    <ul class="list-group w-50 row justify-content-center mx-auto mt-3" aria-labelledby="list-summary">
      <li class="list-group-item" v-for="item in ToDoItems" :key="item.id">
        <to-do-item :label="item.label" :done="item.done" :id="item.id" @checkbox-changed="updateDoneStatus(item.id)"
                                                                        @item-deleted="deleteToDo(item.id)"
                                                                        @item-edited="editToDo(item.id, $event)"></to-do-item>
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
  computed: {
    listSummary() {
      const numberFinishedItems = this.ToDoItems.filter(item =>item.done).length
      return `${numberFinishedItems} out of ${this.ToDoItems.length} items completed`
    }
  },
  methods: {
    addToDo(toDoLabel) {
      this.ToDoItems.push({id: uniqueId('todo-'), label: toDoLabel, done: false })
    },
    updateDoneStatus(toDoId) {
      const toDoToUpdate = this.ToDoItems.find(item => item.id === toDoId)
      toDoToUpdate.done = !toDoToUpdate.done
    },
    deleteToDo(toDoId) {
      this.ToDoItems.splice(this.ToDoItems.findIndex(item => item.id === toDoId), 1)
    },
    editToDo(toDoId, newLabel) {
      this.ToDoItems.find(item => item.id === toDoId).label = newLabel
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
