<template>
  <div class="main">
    <ToDoList />
  </div>
</template>
<script>
// @ is an alias to /src
import ToDoList from "@/components/ToDoApp.vue";

export default {
  name: "HomeView",
  components: { ToDoList },
};
</script>
