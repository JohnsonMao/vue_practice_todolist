<template>
  <div class="input-group bg-white box-shadow rounded-1 overflow-hidden mb-3">
    <input
      type="text"
      class="form-control flex-fill"
      @keyup.enter="handleAdd"
      v-model="newTodo"
      placeholder="新增代辦事項"
    />
    <button
      type="button"
      class="btn btn-size-lg btn-dark rounded-1 m-1"
      @click="handleAdd"
    >
      <i class="fas fa-plus"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "TodoHeader",
  data() {
    return {
      newTodo: ''
    }
  },
  methods: {
    handleAdd() {
      if (!this.newTodo.trim()) return alert("請輸入代辦事項！");
      const todoObj = { id: Date.now(), name: this.newTodo, done: false };
      this.$emit('addTodo', todoObj);
      this.newTodo = "";
    },
  },
};
</script>

<style>
</style>