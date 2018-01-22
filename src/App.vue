<template>
  <div id="app">
    <h1 class="ui dividing centered header">To Do App</h1>
    <div class="ui three column centered grid">
      <div class="column">
        <todo-list v-bind:todos="todos"></todo-list>
        <create-todo v-on:create-todo="createTodo"></create-todo>
      </div>
    </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import axios from 'axios';
import TodoList from './components/TodoList';
import CreateTodo from './components/CreateTodo';

export default {
  name: 'App',
  components: {
    TodoList,
    CreateTodo,
  },
  data() {
    return {
      todos: [{
        name: '',
        endDate: new Date(),
      }],
    };
  },
  methods: {
    createTodo(newTodo) {
      this.todos.push(newTodo);
      sweetalert('Sucess!', 'To-Do created!', 'success');
    },
  },
  created() {
    axios.get('http://front-test.tide.mx/api/tasks')
      .then((response) => {
        this.todos = response.data;
      });
  },
};
</script>

<style>

</style>
