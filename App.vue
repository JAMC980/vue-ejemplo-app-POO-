<template>
  <div>
    <div id="header"></div>
      <Search v-on:query-change="querySearch" />
    <div id="main-container">
      <h2>Todos</h2>
      <Todoadd v-on:add-todo="AddTodo" />
        <Todos v-bind:todoslist="copyTodos" v-on:delete-todo="deleteTodo"/>
    </div>

  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'

import Search from './components/Search';
import Todos from './components/Todos';
import Todoadd from './components/Todoadd';

export default {
  name: 'App',
  components: {
    Todos, Todoadd, Search
  },
  methods:{
    deleteTodo(id){
      this.Todos = this.todos.filter(todo => todo.id != id);
      this.copyTodos = [...this.todos];
    },
    AddTodo(todo){
      this.todos.push(todo);
      this.copyTodos = [...this.todos];
    },
    querySearch(query){
      if(query.trim()== ''){
        this.copyTodos = [...this.todos];
      }else{
        const temp = this.todos.filter(todo =>{
          return todo.title.includes(query)
        });

        this.copyTodos = [...temp];
      }
    }
  },
  data(){
    return{
      Todos: [
        {
          id: 0,
          title: 'comprar la cena',
          completed: false
        },
        {
          id: 1,
          title: 'sacar a pasear al perro',
          completed: true

        },
        {
          id: 2,
          title: 'Descansar',
          completed: false
        },
        {
          id: 3,
          title: 'quemar basura',
          completed: true
        }
      ],
      copyTodos: []
    }
  },
  created(){
    this.copyTodos = [...this.Todos];
  }
}
</script>

<style>
  *{
    box-sizing: border-box;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1.5em;
    padding: 0;
    margin: 0;
  }

  #main-container{
    border: solid 1px #ccc;
    width: 600px;
    margin: 100px auto;
  }
  
  #header{
    background: black;
    padding: 10px;
  }

  h2{
    padding: 0 10 px;
  }
</style>
