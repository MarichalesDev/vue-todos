<template>
  <div>
    <div id="header">
      <Search v-on:query-change="querySearch"/>
    </div>
    
    <div id="main-container"> 
        <h2>Todos</h2>
        <TodoAdd v-on:add-todo="addTodo"/>
        <Todos v-bind:todosList="copyTodos" v-on:delete-todo="deleteTodo"/>
    </div>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Search from './components/Search.vue';
import Todos from './components/Todos.vue';
import TodoAdd from './components/TodoAdd.vue';

export default {
  name: 'App',
  components: {
     Todos, TodoAdd, Search
  },
  methods: {
    deleteTodo (id) {
      this.todos = this.todos.filter(todo => todo.id !== id);
      this.copyTodos = [...this.todos]
    },
    addTodo (todo) {
      this.todos.push(todo);
      this.copyTodos = [...this.todos]
    },
    querySearch (query) {
      if (query.trim() === ''){
        this.copyTodos = [...this.todos]
      }else {
        const temp = this.todos.filter(todo => {
          return todo.title.includes(query)
        });

        this.copyTodos = [...temp]
      }  
    }
  },
  data(){
    return {
      todos: [
        {
          id: 0,
          title: "comprar la cena",
          completed: false
        },
        {
          id: 1,
          title: "sacar a pasear",
          completed: true
        },
        {
          id: 2,
          title: "jugar Xbox",
          completed: false
        },
        {
          id: 3,
          title: "terminar tutorial",
          completed: true
        }
      ],
      copyTodos: []
    }
  },
  created() {
    this.copyTodos = [...this.todos]
  }
  
}
</script>

<style>
 *{
  box-sizing: border-box;
 }

 body {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 1.5em;
  padding: 0;
  margin: 0;
 }

 #main-container {
  border: solid 1px #ccc;
  width: 600px;
  margin: 100px auto; 
 }

 #header {
  background: black;
  padding: 10px;
 }
</style>
