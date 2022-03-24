<template>
  <label
    @click="taskDone(toDo.id)"
    :class="{ taskDone: toDo.state }"
    :checked="toDo.state == true"
    >{{ toDo.text }}</label
  ><input :class="{ taskRemove: toDo.state }" :checked="toDo.state == true" />
</template>

<script>
import { inject } from "@vue/runtime-core";
export default {
  props: {
    toDo: {
      type: Object,
      required: true,
    },
  },
  setup() {
    const toDos = inject("toDos");
    const taskRemove = (id) => {
      toDos.value = toDos.value.filter((item) => item.id !== id);
      //console.log(toDos);
    };
    const taskDone = (id) => {
      toDos.value = toDos.value.map((item) => {
        if (item.id === id) {
          item.state = !item.state;
        }
        return item;
      });
    };
    return { taskRemove, taskDone };
  },
};
</script>
