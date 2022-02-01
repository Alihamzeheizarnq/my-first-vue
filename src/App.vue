<script>
import Content from './components/content.vue';
import Header from './components/header.vue';

export default {
  components: {
    'todo-header': Header,
    Content
  },
  data() {
    return {
      todos: []
    };
  },

  methods: {
    createTodo(text) {
      this.todos = [
        {id: this.todos.length + new Date().getTime(), name: text, done: false},
        ...this.todos
      ];
    },
    chageTodoDone(todo) {
      this.todos = this.todos.filter((item) => {
        if (todo.id == item.id) {
          item.done = !item.done;
        }
        return item;
      });
    },
    deleteTodo(todo) {
      this.todos = this.todos.filter((item) => item != todo);
    },
    editTodo(obj) {
      this.todos = this.todos.filter((item) => {
        if (item.id == obj.id) {
          item.name = obj.text;
        }
        return item;
      });
    }
  }
};
</script>

<template>
  <todo-header> </todo-header>

  <content
    :todos="todos"
    @create-todo="createTodo($event)"
    @done-change-status="chageTodoDone"
    @delete-to="deleteTodo"
    @edit-todo="editTodo"></content>
  <main></main>
</template>

<style></style>
