<template>
  <div class="items">
    <ToDoItem v-for="toDo in filter" :key="toDo.id" :toDo="toDo" />
    <!-- <label v-else>No elements</label> -->
    <ToDoFooter />
    <ToDoFilter />
  </div>
</template>
<script>
import ToDoItem from "@/components/ToDoItem.vue";
import ToDoFooter from "@/components/ToDoFooter.vue";
import ToDoFilter from "@/components/ToDoFilter.vue";
import { inject, ref, computed, provide } from "@vue/runtime-core";
export default {
  components: { ToDoItem, ToDoFooter, ToDoFilter },
  setup() {
    const toDos = inject("toDos");
    const state = ref("all");
    const filter = computed(() => {
      if (state.value === "all") {
        return toDos.value;
      }
      if (state.value === "active") {
        return toDos.value.filter((item) => item.state === false);
      }
      if (state.value === "done") {
        return toDos.value.filter((item) => item.state === true);
      }
    });
    provide("state", state);
    return { filter };
  },
};
</script>

<style></style>
