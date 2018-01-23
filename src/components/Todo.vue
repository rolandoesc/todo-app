<template>
  <div class="ui centered card">
      <div class="content" v-show="!isEditing">
          <div class="header">
              {{ todo.name }}
          </div>
          <div class="meta">
              {{ todo.endDate }}
          </div>
          <div class="extra content">
              <span class="right floated edit icon" v-on:click="showForm">
                  <i class="edit icon"></i>
              </span>
              <span class="right floated trash icon" v-on:click="deleteTodo(todo)">
                  <i class="trash icon"></i>
              </span>
          </div>
      </div>
      <div class="content" v-show="isEditing">
          <div class="ui form">
              <div class="field">
                  <label>Title</label>
                  <input type="text" v-model="todo.name">
              </div>
              <div class="field">
                  <label>Due date</label>
                  <datepicker v-model="todo.endDate"></datepicker>
              </div>
              <div class="ui two button attached buttons">
                  <button class="ui basic blue button" v-on:click="hideForm">
                      Close X
                  </button>
              </div>
          </div>
      </div>
      <div class="ui bottom attached green basic button" v-show="!isEditing && todo.done" disabled>
          Completed
      </div>
      <div class="ui bottom attached red basic button"
      v-on:click="completeTodo(todo)" v-show="!isEditing && !todo.done">
          Pending
      </div>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker';

export default {
  props: ['todo'],
  components: {
    Datepicker,
  },
  data() {
    return {
      isEditing: false,
    };
  },
  methods: {
    completeTodo(todo) {
      this.$emit('complete-todo', todo);
    },
    deleteTodo(todo) {
      this.$emit('delete-todo', todo);
    },
    showForm() {
      this.isEditing = true;
    },
    hideForm() {
      this.isEditing = false;
    },
  },
};
</script>

<style>

</style>
