<template>
  <section class="jumbotron">
    <div class="container d-flex flex-column align-items-center">
      <h1 class="jumbotron-heading">Welcome!</h1>
      <p class="lead text-muted">
        To get started, add some items to your list:
      </p>
      <div class="form-inline">
        <div class="form-group">
          <input
            type="text"
            class="form-control mx-sm-3"
            placeholder="I want to do ..."
            v-model="text" />
          <button
            class="btn btn-primary"
            @click="
              $emit('store-todo', text);
              text = '';
            ">
            add
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  emits: ['store-todo'],
  data() {
    return {
      text: ''
    };
  }
};
</script>
