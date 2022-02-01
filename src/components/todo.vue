<template>
  <div class="col-6 mb-2">
    <div
      class="
        d-flex
        justify-content-between
        align-items-center
        border
        rounded
        p-3
      ">
      <div v-if="!edit">{{ todo.name }}</div>

      <input v-if="edit" type="text" v-model="text" />
      <div>
        <template v-if="!edit">
          <button
            :class="{
              btn: true,
              'btn-success': !todo.done,
              'btn-danger': todo.done,
              'btn-sm': true,
              'mr-1': true
            }"
            @click="$emit('change-status', todo)">
            {{ todo.done == true ? 'undone' : 'done' }}
          </button>
          <button class="btn btn-info btn-sm" @click="edit = true">edit</button>
          <button
            class="btn btn-danger btn-sm ml-1"
            @click="$emit('delete-todo', todo)">
            delete
          </button>
        </template>

        <template v-if="edit">
          <button
            class="btn btn-info btn-sm"
            @click.enter="
              $emit('edit-request', {text, id: todo.id});
              edit = false;
            ">
            Ok
          </button>
        </template>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['change-status', 'delete-todo', 'edit-request'],
  props: ['todo'],
  data() {
    return {
      edit: false,
      text: this.todo.name
    };
  }
};
</script>