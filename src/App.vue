<template>
  <div id="app" class="mx-72 my-12">
    <div class=" mb-6 flex items-center">
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
        @toggleCompleteTask="toggleCompleteTask($event)"
      />
    </template>
  </div>
</template>

<script>
import Task from "./components/Task.vue";
import axios from "axios";

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
        const response = await axios.get(
          "https://10hivotppf.execute-api.us-east-1.amazonaws.com/dev"
        );
        this.tasks = response.data.todos;
      } catch (error) {
        console.log(error);
        this.isError = true;
        this.tasks = [];
      }
    },
    async updateTask(task) {
      const response = await axios.post(
        "https://10hivotppf.execute-api.us-east-1.amazonaws.com/dev",
        task
      );
      this.tasks = this.tasks.map((task) => {
        if (task.id === response.data.id) {
          return response.data;
        } else {
          return task;
        }
      });
    },
    async toggleCompleteTask(taskId) {
      const taskToUpdate = this.tasks.find((task) => task.id === taskId);
      taskToUpdate.isComplete = !taskToUpdate.isComplete;
      try {
        await this.updateTask(taskToUpdate);
      } catch (error) {
        this.isError = true;
        taskToUpdate.isComplete = !taskToUpdate.isComplete;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
