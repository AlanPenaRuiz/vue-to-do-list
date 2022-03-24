<template>
  <h2 class="done" aria-hidden="true" @click="filter('done')">Done</h2>
  <h2 class="undone" aria-hidden="true" @click="filter('active')">
    In Progress
  </h2>
  <div class="filter">
    <button @click="filter('all')">All</button>
    <button @click="filter('active')">Actives</button>
    <button @click="filter('done')">Done</button>
  </div>
</template>
<script>
import { inject } from "@vue/runtime-core";
export default {
  setup() {
    const state = inject("state");
    //console.log(state.value)
    const filter = (value) => {
      state.value = value;
    };

    return { filter };
  },
};
</script>
