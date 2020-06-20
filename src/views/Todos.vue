<template>
  <div>
    <h2>Todo Aplication vue</h2>
    <AddTodo @add-todo="addTodo" />
    <router-link to="/">Home</router-link>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="not-completed">Not-completed</option>
    </select>
    <hr />
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <span v-else>Not todos</span>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import AddTodo from "@/components/AddTodo";
import Loader from "@/components/Loader";

export default {
  name: "App",
  data() {
    return {
      todos: [],
      loading: true,
      filter: "all"
    };
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos/")
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          this.todos = json;
          this.loading = false;
        }, 5000);
      })
  },
  //   watch:{
  //    filter(value){
  //        console.log(value)

  //    }
  computed: {
    filteredTodos() {
      if (this.filter === "all") {
        return this.todos;
      }
      if (this.filter === "completed") {
        return this.todos.filter(p => p.completed);
      }
      if (this.filter === "not-completed") {
        return this.todos.filter(p => !p.completed);
      }
      else {return null}
    }
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
    },
    addTodo(todo) {
      this.todos.push(todo);
      
      
    }
  },
  components: {
    TodoList,
    AddTodo,
    Loader
  }
};
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
