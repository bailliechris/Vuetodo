<template>
  <div id="app">
    <Header />
    <Addtodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from "./components/Todos";
import Header from "./components/Header";
import Addtodo from "./components/Addtodo";
import axios from "axios";

export default {
  name: 'app',
  components: {
    Header,
    Todos,
    Addtodo
  },
  data() {
    return {
      todos: []//End todos array
    }//End return
  },//End data
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(todo => todo.id !== id)
      axios.put("https://api.myjson.com/bins/fijd4", JSON.stringify(this.todos))
    },

    addTodo(newTodo){
      const { title, completed } = newTodo;

      axios.post("https://api.myjson.com/bins/fijd4", JSON.stringify({ title, completed }))
      .then(res => this.todos = [...this.todos, res.data]);
    }
  },
  created() {
    axios.get("https://api.myjson.com/bins/fijd4")
    .then(res => this.todos = res.data);
  }
}
</script>

<style>
* {
  box-sizing:border-box;
  margin:0;
  padding:0;
}

body{
  font-family:Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display:inline-block;
  border: none;
  background: darkslategrey;
  color:white;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover{
  background:orange;
}
</style>
