<template>
  <div>
      <p class="tasks">
        Completed Tasks: {{ myTodos.filter(todo => { return todo.done === true}).length }}
      </p>
      <p class="tasks">
        Pending Tasks: {{ myTodos.filter(todo => { return todo.done === false}).length }}
      </p>
      <div class="content">
        <div v-for="list in myLists" :key="list.creationDate">
          <h3 class="header tasks">{{ list.name }}</h3>
        </div>
        <todo v-on:delete-todo="deleteTodo"
        v-on:complete-todo="completeTodo"
        v-for="todo in myTodos" :todo.sync="todo" :key="todo.creationDate">
        </todo>
      </div>
  </div>
</template>

<script>
import sweetalert from 'sweetalert';
import Todo from './Todo';

export default {
  props: ['myTodos', 'myLists'],
  components: {
    Todo,
  },
  methods: {
    deleteTodo(todo) {
      sweetalert({
        title: 'Are you sure?',
        text: 'This To-Do will be permanently deleted!',
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#DD6B55',
        confirmButtonText: 'Yes, delete it!',
        closeOnConfirm: false,
      },
      () => {
        const todoIndex = this.myTodos.indexOf(todo);
        this.myTodos.splice(todoIndex, 1);
        sweetalert('Deleted!', 'Your To-Do has been deleted.', 'success');
      });
    },
    completeTodo(todo) {
      const todoIndex = this.myTodos.indexOf(todo);
      this.myTodos[todoIndex].done = true;
      sweetalert('Success!', 'To-Do completed!', 'success');
    },
  },

};
</script>

<style scoped>
p.tasks {
    text-align: center;
}
</style>
