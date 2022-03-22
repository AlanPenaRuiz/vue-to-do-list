<template>
  <li>
    <span @click="taskDone(toDo.id)" :class="{ taskDone: toDo.state }">{{
      toDo.text
    }}</span
    ><span @click="taskRemove(toDo.id)" :class="{ taskRemove: toDo.state }">
      <svg viewBox="0 0 352 512" width="50" height="25">
        <path
          d="M242.72 256l100.07-100.07c12.28-12.28 12.28-32.19 0-44.48l-22.24-22.24c-12.28-12.28-32.19-12.28-44.48 0L176 189.28 75.93 89.21c-12.28-12.28-32.19-12.28-44.48 0L9.21 111.45c-12.28 12.28-12.28 32.19 0 44.48L109.28 256 9.21 356.07c-12.28 12.28-12.28 32.19 0 44.48l22.24 22.24c12.28 12.28 32.2 12.28 44.48 0L176 322.72l100.07 100.07c12.28 12.28 32.2 12.28 44.48 0l22.24-22.24c12.28-12.28 12.28-32.19 0-44.48L242.72 256z"
        />
      </svg>
    </span>
  </li>
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
          item.state = true;
        }
        return item;
      });
    };
    return { taskRemove, taskDone };
  },
};
</script>

<style>
.taskDone {
  text-decoration: line-through;
}
</style>
