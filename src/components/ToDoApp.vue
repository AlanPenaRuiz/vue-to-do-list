<template>
  <div class="container">
    <h1>LIST</h1>
    <ToDoForm />
    <ToDoList />
  </div>
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

    if (localStorage.getItem("toDos")) {
      toDos.value = JSON.parse(localStorage.getItem("toDos"));
    }
    watchEffect(() => {
      //console.log("Nº: ", toDos.value.length);
      //console.log(toDos.value);
      localStorage.setItem("toDos", JSON.stringify(toDos.value));
    });
  },
};
</script>

<style lang="scss">
@import url(https://fonts.googleapis.com/css?family=Roboto:500,700);

*,
*::before,
*::after {
  box-sizing: border-box;
}

html {
  min-height: 100%;
}

body {
  margin: 20px;
  color: #435757;
  background: linear-gradient(-20deg, #d0b782 20%, #a0cecf 80%);
  font: 500 1.2em/1.2 "Roboto", sans-serif;
}

.container {
  max-width: 450px;
  margin: 0 auto;
  border-top: 5px solid #435757;
  background-color: rgba(255, 255, 255, 0.2);
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  user-select: none;
}

h1 {
  margin: 0;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.4);
  font-size: 1.8em;
  text-align: center;
}

.items {
  display: flex;
  flex-direction: column;
  padding: 20px;
  counter-reset: done-items undone-items;
}

h2 {
  position: relative;
  margin: 0;
  padding: 10px 0;
  font-size: 1.2em;
}

h2::before {
  content: "";
  display: block;
  position: absolute;
  top: 10px;
  bottom: 10px;
  left: -20px;
  width: 5px;
  background-color: #435757;
}

h2::after {
  display: block;
  float: right;
  font-weight: normal;
}

.info-tasks {
  font-size: 22px;
}

.filter {
  display: flex;
  margin: 5% 0;
}

$col-primary: #00c7ec;

button {
  text-transform: uppercase;
  text-align: center;
  color: $col-primary;
  border: 1px solid $col-primary;
  border-radius: 5px;
  line-height: 3em;
  width: 100%;
  cursor: pointer;
  box-shadow: 0 0 0 0 transparent;
  transition: all 0.2s ease-in;
  background: none;
  margin: 0 2px;

  &.btn-rm {
    color: darkred;
    border: 1px solid red;
    margin-top: 25px;
    order: 5;
    &:hover {
      box-shadow: 0 0 30px 0 transparentize(red, 0.5);
      background-color: red;
    }
  }

  &:hover {
    color: white;
    box-shadow: 0 0 30px 0 transparentize($col-primary, 0.5);
    background-color: $col-primary;

    transition: all 0.2s ease-in;

    &:before {
      animation: shine 0.5s 0s linear;
    }
  }

  &:active {
    box-shadow: 0 0 0 0 transparent;
    transition: box-shadow 0.2s ease-in;
  }

  &:before {
    content: "";
    display: block;
    width: 0px;
    height: 86%;
    position: absolute;
    top: 7%;
    left: 0%;

    opacity: 0;
    background: white;
    box-shadow: 0 0 15px 3px white;
    transform: skewX(-20deg);
  }
}

@keyframes (shine) {
  from {
    opacity: 0;
    left: 0%;
  }

  50% {
    opacity: 1;
  }
  to {
    opacity: 0;
    left: 100%;
  }
}

.done {
  order: 3;
}

.done::after {
  content: " (" counter(done-items) ")";
}

.undone {
  order: 1;
}

.undone::after {
  content: " (" counter(undone-items) ")";
}

input {
  display: none;
  height: 53px;
  margin: 0 0 -53px -9999px;
  order: 4;
  outline: none;
}

input.main-input {
  all: unset;
  margin-top: 15px;
  height: 30px;
  width: 80%;
  background-color: rgb(255 255 255 / 25%);
  border-radius: 15%;
}

input:checked {
  order: 2;
  counter-increment: done-items;
}

label {
  display: block;
  position: relative;
  padding: 15px 0 15px 45px;
  border-top: 1px dashed #fff;
  order: 2;
  cursor: pointer;
  animation: undone 0.5s;
  counter-increment: undone-items;
  color: darkred;
  text-align: initial;
}

label::before {
  display: block;
  content: " ";
  background-image: url("../assets/uncheck.svg");
  background-size: 28px 28px;
  height: 28px;
  width: 28px;
  position: absolute;
  top: 11px;
  left: 10px;
}

label.taskDone {
  text-decoration: line-through;
  order: 4;
  counter-increment: done-items;
  color: darkgreen;
}

label.taskDone::before {
  display: block;
  content: " ";
  background-image: url("../assets/check.svg");
  background-size: 28px 28px;
  height: 28px;
  width: 28px;
  position: absolute;
  top: 11px;
  left: 10px;
}

label:hover,
input:focus + label {
  background-color: rgba(255, 255, 255, 0.2);
}

input:checked + label {
  order: 2;
  animation: done 0.5s;
}

input:checked + label::before {
  content: "\f058"; /* circle checkmark */
}

@keyframes done {
  0% {
    opacity: 0;
    background-color: rgba(255, 255, 255, 0.4);
    transform: translateY(20px);
  }
  50% {
    opacity: 1;
    background-color: rgba(255, 255, 255, 0.4);
  }
}

@keyframes undone {
  0% {
    opacity: 0;
    background-color: rgba(255, 255, 255, 0.4);
    transform: translateY(-20px);
  }
  50% {
    opacity: 1;
    background-color: rgba(255, 255, 255, 0.4);
  }
}
</style>
