<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <!-- <TaskInput @add-task="addNewTask" @mention-name="sayMyName" /> -->
  <!-- <Counter @counter-event="incrCounter" /> -->
  <div id="app">
    <CurrentTime class="col-4" />
    <task-input class="col-6" @add-task="addNewTask" />
    <div class="col-12">
      <div class="cardBox">
        <ul class="taskList">
          <li
            v-for="(taskItem, index) in displayList"
            :key="`${index}_${Math.random()}`"
          >
            <input
              type="checkbox"
              :checked="!!taskItem.finishedAt"
              @input="changeStatus(index)"
            />
            {{ taskItem.task }}
            <span v-if="taskItem.finishedAt">
              | Done at: {{ formatDate(taskItem.finishedAt) }}</span
            >
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import TaskInput from "./components/TaskInput.vue";
// import Counter from "./components/Counter.vue";
import CurrentTime from "./components/CurrentTime.vue";

export default {
  name: "App",
  components: {
    TaskInput,
    // Counter,
    CurrentTime,
  },

  data() {
    return {
      counter: 0,
      taskList: [],
    };
  },
  computed: {
    displayList() {
      // return this.taskList.filter((taskItem) => !taskItem.finishedAt);
      return this.taskList;
    },
  },

  methods: {
    formatDate(value) {
      if (!value) return "";
      if (typeof value !== "number") return value;
      const browserLocale =
        navigator.languages && navigator.languages.length
          ? navigator.languages[0]
          : navigator.language;
      const intlDateTime = new Intl.DateTimeFormat(browserLocale, {
        year: "numeric",
        month: "numeric",
        day: "numeric",
        hour: "numeric",
        minute: "numeric",
      });
      return intlDateTime.format(new Date(value));
    },

    addNewTask(task) {
      this.taskList.push({
        task,
        createdAt: Date.now(),
        finishedAt: undefined,
      });
    },

    changeStatus(taskIndex) {
      const task = this.taskList[taskIndex];
      if (task.finishedAt) {
        task.finishedAt = undefined;
      } else {
        task.finishedAt = Date.now();
      }
    },

    sayMyName(name) {
      alert(`Hello, Welcome ${name}`);
    },

    incrCounter() {
      this.counter++;
      alert(`Counter: ${this.counter}`);
    },
  },
};
</script>

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.taskList li {
  text-align: left;
}
</style>
