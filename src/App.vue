<template>
  <ToDoList />
</template>

<script>
import ToDoList from "./components/ToDoList.vue";
export default {
  name: "App",
  components: {
    ToDoList,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;

  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  padding: 20px;
}
</style>
