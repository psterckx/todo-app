<template>
  <div id="app" class="mx-72 my-12">
    <h1 class="text-xl mb-6">My Tasks</h1>
    <Task
      v-for="task in tasks"
      :key="task.id"
      :id="task.id"
      :name="task.name"
      :isComplete="task.isComplete"
      @toggleCompleteTask="toggleCompleteTask($event)"
    />
  </div>
</template>

<script>
import Task from "./components/Task.vue";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: [
        {
          id: "1643376797940",
          name: "Make coffee",
          isComplete: false,
        },
        {
          id: "1643376801982",
          name: "Hack",
          isComplete: true,
        },
        {
          id: "1643376814350",
          name: "Make more coffee",
          isComplete: false,
        },
      ],
    };
  },
  methods: {
    toggleCompleteTask(taskId) {
      console.log(taskId);
      const taskToUpdate = this.tasks.find((task) => task.id === taskId);
      taskToUpdate.isComplete = !taskToUpdate.isComplete;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>
