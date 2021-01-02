<template>
  <div id="app">
    <AddTodo @add-Todo="addTodo" />
    <Todos v-bind:todos="todos" @del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";

export default {
  name: 'Home',
  components: {
    Todos, AddTodo
  },
  data(){
    return {
      todos: []
    }
  },
  methods:{
    deleteTodo(id){
      fetch(`https://jsonplaceholder.typicode.com/todos${id}`, {
        method: 'DELETE',
      })
      .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(error => alert('Error:', error))
    },
    addTodo(newTodo){
      const {title, completed} = newTodo
      fetch('https://jsonplaceholder.typicode.com/todos', {
        method: 'POST', // or 'PUT'
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({title, completed}),
      })
      .then(response => response.json())
      .then(data => this.todos = [...this.todos, data])
      .catch(error => alert('Error:', error))
    }
  },
  created(){
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
      .then(response => response.json())
      .then(data => {
        this.todos = data
        console.log(data);
      })
      .catch(err => alert(`ERROR: ${err.name} - ${err.message}`))
  }
}
</script>

<style>
  
</style>