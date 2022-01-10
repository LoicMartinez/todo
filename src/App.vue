<template>
  <div id="app">
    <h1>My todo List</h1>
    <TotalSlot>{{todos.length}} Tâches</TotalSlot>
    <Todo
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        @started="started"
        @ended="ended">

    </Todo>
    <div>
      <label>Nouvelle tâche</label>
      <input type="text" v-model="this.newTodo">
      <button @click="addTodo(this.newTodo)">Ajouter</button>
    </div>
  </div>
</template>

<script>
import TotalSlot from '@/components/TotalSlot'
import Todo from '@/components/Todo'

export default {
  name: 'App',
  components: {
    TotalSlot,
    Todo,
  },
  data() {
    return {
      todos: [],
      newTodo: '',
    }
  },
  mounted() {
    this.$http.get('http://localhost:3000/todos')
    .then(response => {
      console.log(response)
      this.todos = response.body;
    }, error => {
      console.log(error);
    })
  },
  methods: {
    addTodo(desc) {
      let id = this.todos.length+1;
      let todo = {id: id, nom: 'my-todo', desc: desc, statut: 'waiting'};
      this.$http.post('http://localhost:3000/todos', todo)
      this.newTodo = '';
      console.log(todo)
    },
    chgStatut: function(id, newStatut) {
      this.todos.forEach(elem => {
        if(elem.id === id)
          this.$http.put('http://localhost:3000/todos')
          elem.statut = newStatut;
      })
    },
    started(id) {
      console.log('started' + id)
      this.chgStatut(id, 'started')
    },
    ended(id) {
      console.log('ended' + id)
      this.chgStatut(id, 'ended')
    }
  }
}
</script>

<style>
Todo {
  margin-bottom: 20px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  margin-bottom: 100px;
}
</style>
