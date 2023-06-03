<template>
  <div class="cardBox">
    <div class="container tasker">
      <strong>Todo List </strong>
      <input type="text" v-model="task" class="taskInput" />
      <button v-on:click="addTask">Add Task</button>
    </div>

    <!-- <div>
      <strong>Say my name</strong>
      <input
        type="text"
        :value="name"
        @input="name = $event.target.value"
        class="taskInput"
      />
      <button v-on:click="mentionName">Mention my name</button>
    </div> -->
  </div>
</template>

<script>
export default {
  name: "TaskInput",
  data: () => ({
    task: "",
    name: "",
  }),

  methods: {
    addTask() {
      this.$emit("add-task", this.task);
      this.task = "";
    },
    mentionName() {
      this.$emit("mention-name", this.name);
      this.name = "";
    },
  },
};
</script>
