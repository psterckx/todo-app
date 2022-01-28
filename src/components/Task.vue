<template>
  <div class="flex items-center my-2">
    <input type="checkbox" :checked="isComplete" @change="toggleCompleteTask" />
    <div v-if="!isComplete" class="text-lg ml-2">{{ name }}</div>
    <div v-else class="text-lg text-gray-500 ml-2">
      <s>
        {{ name }}
      </s>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    id: String,
    name: String,
    isComplete: Boolean,
  },
  methods: {
    toggleCompleteTask() {
      this.$emit("toggleCompleteTask", this.id);
    },
  },
};
</script>
