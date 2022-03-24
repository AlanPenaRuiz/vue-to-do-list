<template>
  <div class="info-tasks">Active tasks: {{ activeTasks }}</div>
  <button class="btn-rm" @click="removeActTasks">Remove completed tasks</button>
</template>

<script>
import { computed, inject } from "vue";
export default {
  setup() {
    const toDos = inject("toDos");
    const activeTasks = computed(() => {
      return toDos.value.filter((item) => item.state === false).length;
    });
    const removeActTasks = () => {
      toDos.value = toDos.value.filter((item) => item.state === false);
    };
    return { activeTasks, removeActTasks };
  },
};
</script>
