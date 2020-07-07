<template>
<div class="app">
  <Header  />
  <AddToDo v-on:add-todo="addTodo" />
  <Todos :todos="todos" v-on:del-todo="deleteToDo" />
</div>
</template>

<script>
import Todos from './components/Todos'
import Header from './components/layout/Header'
import AddToDo from './components/AddToDo'
import axios from 'axios'
export default {
  name: "App",
  components: {
    Todos,
    Header,
    AddToDo
  },
  data() {
    return {
      todos: []
    };
  },
  methods: {
    deleteToDo(id) {
      this.todos = this.todos.filter(t=> t.id !== id)
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res=> this.todos = [...this.todos, res.data])
      .catch(e=> console.log(e))
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=10')
      .then(res => this.todos = res.data)
      .catch(e=> console.log(e))
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
.btn{
  border: none;
  background-color: grey;
  padding: 10px 15px;
  cursor: pointer;
}
</style>
