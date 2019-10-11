<template>
  <div class="mt-3 text-center col-md-6 offset-md-3">
    <div v-show="error" class="alert alert-warning alert-dismissible fade show" role="alert">
      <strong>Oops!</strong> You cannot modify completed todos.
      <button
        type="button"
        class="close"
        data-dismiss="alert"
        aria-label="Close"
      >
        <span aria-hidden="true">&times;</span>
      </button>
    </div>
    <div class="d-flex justify-content-between" v-if="!editing">
      <p v-bind:class="{'is-complete' : todo.status == true}" @dblclick="editMode(todo)">
        <input type="checkbox" :checked="todo.status == true" @change="markComplete(todo)" />
        {{todo.title}}
      </p>
      <button class="btn btn-sm btn-outline-danger rounded-circle" @click="$emit('del',todo)">X</button>
    </div>
    <div class="d-flex justify-content-between" v-else>
      <input
        type="text"
        class="form-control outline"
        @keyup.esc="cancelEdit"
        v-model="title"
        @blur="cancelEdit"
        @keyup.13="updateTodo"
        v-focus
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "Todo",
  props: {
    todo: {
      required: true,
      type: Object
    }
  },
  data() {
    return {
      editing: false,
      id:this.todo.title,
      title: this.todo.title,
      error: false
    };
  },
  methods: {
    markComplete(todo) {
      todo.status = !todo.status;
    },
    editMode(todo) {
      if (todo.status == true) {
        this.error = true;
        return;
      }
      this.editing = true;
    },
    cancelEdit() {
      this.editing = false;
    },
    updateTodo(){
        const UpdatedTodo = {
            id:this.id,
            title:this.title,
            status:false,
        };
        this.$emit('update',UpdatedTodo);
    }
  },

  directives: {
    focus: {
      inserted: function(el) {
        el.focus();
      }
    }
  }
};
</script>

<style scoped>
.is-complete {
  text-decoration: line-through;
  color: red;
}

input[type="text"]:focus {
  outline: 0 !important;
  outline-color: #fff !important;
  border: none !important;
  box-shadow: inset 0 -1px 0 #fff !important;
  border-bottom: 1px solid #000 !important;
  transition: 1s all;
  border-radius: 0px !important;
  transition-timing-function: ease-in-out;
}
</style>