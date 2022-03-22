<template>
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
