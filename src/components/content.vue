<template>
  <todo-create @store-todo="$emit('create-todo', $event)"></todo-create>

  <div class="todoList">
    <div class="container">
      <div class="d-flex flex-column align-items-center">
        <nav class="col-6 mb-3">
          <div class="nav nav-tabs" id="nav-tab" role="tablist">
            <a
              class="nav-item nav-link font-weight-bold"
              :class="{active: status == 'undone'}"
              id="nav-home-tab"
              @click="status = 'undone'">
              undone
              <span class="badge badge-secondary">{{
                todoListunDone.length
              }}</span>
            </a>
            <a
              class="nav-item nav-link font-weight-bold"
              :class="{active: status == 'done'}"
              id="nav-profile-tab"
              @click="status = 'done'">
              done
              <span class="badge badge-success">{{ todoListDone.length }}</span>
            </a>
          </div>
        </nav>

        <template v-if="status === 'done'">
          <todo
            v-for="todo in todoListDone"
            :todo="todo"
            :key="todo.id"
            @delete-todo="$emit('delete-to', $event)"
            @edit-request="$emit('edit-todo', $event)"
            @change-status="$emit('done-change-status', $event)">
          </todo>
        </template>

        <template v-if="status === 'undone'">
          <todo
            v-for="todo in todoListunDone"
            :todo="todo"
            :key="todo.id"
            @delete-todo="$emit('delete-to', $event)"
            @edit-request="$emit('edit-todo', $event)"
            @change-status="$emit('done-change-status', $event)">
          </todo>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import Create from './create.vue';
import Todo from './todo.vue';
export default {
  emits: ['create-todo', 'done-change-status', 'delete-to', 'edit-todo'],
  props: ['todos'],

  data() {
    return {
      status: 'undone' //done or undone
    };
  },
  components: {
    'todo-create': Create,
    todo: Todo
  },
  computed: {
    todoListDone() {
      return this.todos.filter((item) => item.done);
    },
    todoListunDone() {
      return this.todos.filter((item) => !item.done);
    }
  },
  methods: {
    form(e) {
      console.log(e);
    }
  }
};
</script>