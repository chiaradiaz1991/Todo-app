<template>
  <div class="todo-item" :class="{'is-complete': todo.completed}">
    <input type="checkbox" v-on:change="markedAsCompleted">
    <p>{{todo.title}}</p>
    <button class="del" @click="$emit('del-todo', todo.id)">X</button>
  </div>  
</template>

<script>
export default {
  name:"TodoItem",
  props: ["todo"],
  methods: {
    markedAsCompleted () {
      this.todo.completed = !this.todo.completed
    }
  }
}
</script>

<style scoped>
.todo-item{
  background-color: lightyellow;
  padding: 10px;
  border-bottom: 1px black solid;
  width: 80%;
  margin: auto;
  display: flex;
  justify-content: space-between;
}

.is-complete {
  background-color: lightgreen;
}

.del {
  background-color: pink;
  color: white;
  padding: 5px 9px;
  border-radius: 50%;
}

</style>