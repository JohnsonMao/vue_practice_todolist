<template>
  <li class="input-group">
    <input
      type="text"
      class="form-edit flex-fill"
      v-show="todo.isEdit"
      :value="todo.name"
      ref="inputTitle"
      @blur="finishEdit($event, todo)"
      @keyup.enter="finishEdit($event, todo)"
    />
    <div v-show="!todo.isEdit" class="input-group">
      <input
        type="checkbox"
        class="form-check m-4"
        :id="todo.id"
        :checked="todo.done"
        @change="handleDone(todo.id)"
      />
      <label
        class="flex-fill lh-1 py-4 ms-1"
        :for="todo.id"
        :class="todo.done ? 'del' : ''"
      >
        {{todo.name}}
      </label>
    </div>
    <button
      type="button"
      class="btn btn-size-base list-btn-warning"
      aria-label="Edit"
      v-show="!todo.isEdit"
      @click="handleEdit(todo)"
    >
      <i class="fas fa-pen"></i>
    </button>
    <button
      type="button"
      class="btn btn-size-base list-btn-warning m-3"
      aria-label="Close"
      @click="handleDelete(todo.id)"
    >
      <i class="fas fa-times"></i>
    </button>
  </li>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    handleDone(id) {
      this.$bus.$emit('checkTodo', id);
    },
    handleDelete(id) {
      if (window.confirm("確定刪除嗎？")) {
        this.$bus.$emit('deleteTodo', id)
      }
    },
    handleEdit(todo) {
      if (Object.prototype.hasOwnProperty.call(todo, 'isEdit')) {
        todo.isEdit = true;
      } else {
        this.$set(todo, 'isEdit', true);
      }
      this.$nextTick(function() {
        this.$refs.inputTitle.focus();
      })
    },
    finishEdit(e, todo) {
      todo.isEdit = false;
      if (!e.target.value.trim()) return alert("不能是空白！")
      this.$bus.$emit('updateTodo', todo.id, e.target.value)
    }
  },
};
</script>

<style>
</style>