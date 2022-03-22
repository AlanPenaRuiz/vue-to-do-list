<template>
  <h1>LIST</h1>
  <ToDoForm />
  <ToDoList />
</template>

<script>
import ToDoForm from "@/components/ToDoForm.vue";
import ToDoList from "@/components/ToDoList.vue";
import { ref } from "@vue/reactivity";
import { provide, watchEffect } from "@vue/runtime-core";
export default {
  components: { ToDoForm, ToDoList },
  setup() {
    const toDos = ref([]);
    provide("toDos", toDos);

    watchEffect(() => {
      //console.log("Nº: ", toDos.value.length);
      //console.log(toDos.value);
    });
  },
};
</script>
