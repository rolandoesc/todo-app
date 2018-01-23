<template>
  <div id="app">
    <h1 class="ui dividing centered header">To Do App</h1>
    <div class="ui three column centered grid">
      <div class="column">
        <create-list v-on:create-list="createList"></create-list>
        <todo-list v-for="list in lists" :key="list.creationDate"
        :myTodos="todos" :myLists="lists"></todo-list>
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
import CreateList from './components/CreateList';


export default {
  name: 'App',
  components: {
    TodoList,
    CreateTodo,
    CreateList,
  },
  data() {
    return {
      todos: [],
      lists: [],
    };
  },
  methods: {
    createTodo(newTodo) {
      this.todos.push(newTodo);
      sweetalert('Sucess!', 'To-Do created!', 'success');
    },
    createList(newList) {
      this.lists.push(newList);
      sweetalert('Sucess!', 'List created!', 'success');
    },
  },
  created: function () {
    axios.get('http://front-test.tide.mx/api/task_lists')
      .then((response) => {
        this.lists = response.data;
        this.todos = this.lists[0].tasks;
        this.todos = this.todos.map((el) => {
          const newEl = el;
          newEl.done = false;
          return newEl;
        });
      });
  },
};
</script>

<style>

</style>
