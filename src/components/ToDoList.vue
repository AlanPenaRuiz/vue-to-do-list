<template>
  <ul>
    <ToDoItem v-for="toDo in toDos" :key="toDo.id" :toDo="toDo" />
  </ul>
</template>
<script>
import ToDoItem from "@/components/ToDoItem.vue";
import { inject } from "@vue/runtime-core";
export default {
  components: { ToDoItem },
  setup() {
    const toDos = inject("toDos");
    return { toDos };
  },
};
</script>

<style></style>
