<template>
  <div class="list-frame vh-50">
    <ul class="list-group">
      <transition-group name="fade" appear>
        <TodoItem v-for="todo in todos" :key="todo.id" :todo="todo" />
      </transition-group>
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  components: { TodoItem },
  props: ["todos"],
};
</script>

<style scoped>
.fade-enter-active {
  animation: fade 0.15s;
}
.fade-leave-active {
  animation: fade 0.15s reverse;
}

@keyframes fade {
  from {
    transform: translateX(100%);
    opacity: .4;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}
</style>