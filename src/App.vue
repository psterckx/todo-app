<template>
  <div id="app" class="ml-72 my-12">
    <div class="mb-6 flex items-center">
      <h1 class="text-xl mr-8">My Tasks</h1>
      <div v-if="isError">&#129301; Something's not right...</div>
    </div>
    <template>
      <Task
        v-for="task in tasks"
        :key="task.id"
        :id="task.id"
        :name="task.name"
        :isComplete="task.isComplete"
        @updateTask="updateTask($event)"
      />
    </template>
  </div>
</template>

<script>
import Task from "./components/Task.vue";
import axios from "axios";

// put your url from API Gateway here
const url = "";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: [],
      isError: false,
    };
  },
  created() {
    this.getTasks();
  },
  methods: {
    async getTasks() {
      try {
        const response = await axios.get(url);
        this.tasks = response.data.todos;
      } catch (error) {
        console.log(error);
        this.isError = true;
        this.tasks = [];
      }
    },
    async updateTask(taskId) {
      const taskToUpdate = this.tasks.find((task) => task.id === taskId);
      taskToUpdate.isComplete = !taskToUpdate.isComplete;
      // Uncomment below to make POST request to update a task
      // try {
      //   await axios.post(url, taskToUpdate);
      // } catch (error) {
      //   console.log(error);
      //   this.isError = true;
      //   taskToUpdate.isComplete = !taskToUpdate.isComplete;
      // }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
