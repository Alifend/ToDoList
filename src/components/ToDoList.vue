<template>
  <div class="container">
    <h1>To Do App</h1>
    <h3 class="col-4">New To Do</h3>
    <div>
      <input
        v-model="newtask.content"
        v-on:keyup.enter="AddTask()"
        autofocus
        type="text"
        class="col-12 mb-2"
        id="input"
      />
      <button
        @click="AddTask()"
        type="button"
        class="btn btn-primary col-12 p-2"
      >
        Add To Do
      </button>

      <h3 class="col-12 mt-4">To Do List</h3>
      <hr>
      <div v-for="(task, index) in tasks" :key="index" class="tarjeta size ">
        <div class="container">
          <span
            @click="Change(index)"
            :class="task.done ? 'done' : ''"
            class="m-5"
            style="display:inline"
            >{{ task.content }}</span
          >
          <button
            @click="Remove(index)"
            type="button"
            class="btn btn-danger col-2 "
          >
            Remove
          </button>
        </div>
      </div>
      <div>
        <h3 v-if="isEmpty">
          Empty List
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
import Task from "../models/task.js";
export default {
  data() {
    return {
      newtask: new Task(),
      tasks: [],
    };
  },
  mounted() {
    this.tasks = JSON.parse(localStorage.getItem("data")) || [];
  },
  methods: {
    Change(index) {
      this.tasks[index].done = !this.tasks[index].done;
      this.SaveData();
    },
    AddTask() {
      if (this.newtask.content) {
        console.log(this.newtask, "alkjsdkalsjd");
        this.newtask.done = false;
        this.tasks.push(this.newtask);
        this.SaveData();
        this.newtask = new Task();
        document.getElementById("input").focus();
        console.log(localStorage.getItem("data"));
      }
    },
    Remove(index) {
      this.tasks.splice(index, 1);
      this.SaveData();
      console.log(localStorage.getItem("data"));
    },
    SaveData() {
      const storageData = JSON.stringify(this.tasks);
      localStorage.setItem("data", storageData);
    },
  },

  computed: {
    isEmpty() {
      return 0 == this.tasks.length;
    },
  },
};
</script>

<style scoped>
h1,
h3 {
}
.done {
  text-decoration: line-through;
}
.align {
}

.tarjeta {
  border: 2px solid gray;
  border-radius: 5px;
  padding: 5px;
  margin-bottom: 10px;
}
span {
  cursor: pointer;
}


.size {
  max-width: 600px;
}
</style>
