<template>
  <div class="todo" id="app">
    <div class="todo__header">
      <h4 class="todo__title">TODO-VUE</h4>
    </div>
    <div class="todo__tasks">
      <Task
        v-for="(task, index) in tasks"
        :key="index"
        :index="index"
        :text="task.text"
        :checked="task.completed"
        @onToggleCompleted="onToggleCompleted"
        @onRemoveTask="onRemoveTask"
        @onEditTask="onEditTask"
      />
    </div>
    <TaskField class="todo__task-field" @onAddTask="onAddTask" />
  </div>
</template>

<script>
import Task from "./components/Task";
import TaskField from "./components/TaskField";

export default {
  name: "App",
  components: {
    Task,
    TaskField,
  },
  data: () => ({
    tasks: [],
  }),
  mounted() {
    if (localStorage.tasks) {
      this.tasks = JSON.parse(localStorage.getItem("tasks"));
    } else {
      localStorage.setItem("tasks", JSON.stringify([]));
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler(newTasks) {
        localStorage.setItem("tasks", JSON.stringify(newTasks));
      },
    },
  },
  methods: {
    onToggleCompleted(index) {
      this.tasks[index].completed = !this.tasks[index].completed;
    },
    onAddTask(text) {
      this.tasks.push({ text, completed: false });
    },
    onRemoveTask(index) {
      this.tasks.splice(index, 1);
    },
    onEditTask(index, newText) {
      this.tasks[index].text = newText;
    },
  },
};
</script>

<style>
body {
  background-color: #a4f6cf;
  font-family: "Consolas", Arial, Helvetica, sans-serif;
}
.todo {
  background: #e7ffe6;
  max-width: 530px;
  margin: 70px auto;
  border-radius: 5px;
  overflow: hidden;
  box-shadow: 2px 2px 10px 1px rgba(152, 152, 152, 0.63);
}
.todo__header {
  display: flex;
  align-items: center;
  padding: 0 1rem;
  color: white;
  background-color: #49e198;
  text-align: center;
  text-transform: uppercase;
}
.todo__title {
  display: inline-block;
  color: #e7ffe6;
  margin: 1rem auto;
}
.todo__tasks {
  margin: 20px;
}
.todo__task-field {
  margin: 20px;
}
</style>
