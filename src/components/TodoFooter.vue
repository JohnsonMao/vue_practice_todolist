<template>
  <div class="d-flex justify-content-between mb-2" v-show="total">
    <div class="d-flex align-items-center">
      <!-- toggle all todo -->
      <input
        type="checkbox"
        v-model="handleCheckAll"
        class="form-check m-4"
      />
      <!-- todos scoreboard -->
      <h3 class="text-dark-gray">
        已完成 {{doneCount}} / 全部 {{total}}
      </h3>
    </div>
    <!-- clear all done todo -->
    <button
      type="button"
      @click="handleClearAllDone"
      class="btn btn-text-warning m-4 me-8"
    >
      清除已完成項目
    </button>
  </div>
</template>

<script>
export default {
  name: "TodoFooter",
  props: ['todos'],
  computed: {
    total() {
      return this.todos.length
    },
    doneCount() {
      return this.todos.reduce((pre, current) => pre + (current.done ? 1 : 0), 0);
    },
    handleCheckAll: {
      get() {
        return this.doneCount === this.total && this.total > 0;
      },
      set(value) {
        this.$emit('checkAllTodo', value)
      }
    }
  },
  methods: {
    handleClearAllDone() {
      if (window.confirm("你確定要刪除已完成的任務?")) {
        this.$emit('clearAllDone')
      }
    },
  }
};
</script>

<style>
</style>