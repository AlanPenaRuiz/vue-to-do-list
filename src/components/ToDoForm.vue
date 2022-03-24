<template>
  <form @submit.prevent="form">
    <input
      type="text"
      class="main-input"
      placeholder="Add Task"
      v-model.trim="text"
    />
  </form>
</template>

<script>
import { inject, ref } from "@vue/runtime-core";
export default {
  setup() {
    const toDos = inject("toDos");
    const text = ref("All");
    const form = () => {
      if (text.value === "") {
        console.log("Empty");
        return;
      }
      const toDo = {
        text: text.value,
        state: false,
        id: Date.now(),
      };

      toDos.value.push(toDo);
      text.value = "";
      //console.log("form", toDos.value);
    };
    return { form, text };
    //console.log(todos.value);
  },
};
</script>

<style></style>
