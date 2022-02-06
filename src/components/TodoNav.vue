<template>
  <ul class="btn-group">
    <li class="col" :class="filterType === 'all' ? 'active' : ''">
      <button type="button" class="btn" @click="handleFilter('all')">全部</button>
    </li>
    <li class="col" :class="filterType === 'undone' ? 'active' : ''">
      <button type="button" class="btn" @click="handleFilter('undone')">待完成</button>
    </li>
    <li class="col" :class="filterType === 'done' ? 'active' : ''">
      <button type="button" class="btn" @click="handleFilter('done')">已完成</button>
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoNav",
  props: ['filterType'],
  methods: {
    handleFilter(type) {
      this.$emit('toggleFilter', type)
    }
  },
};
</script>

<style>
</style>