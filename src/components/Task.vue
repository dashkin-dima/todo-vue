<template>
  <div class="task" v-if="isEditing">
    <div class="task__checkbox" v-if="checked" @click="toggleCompleted(index)">
      <svg
        class="svg-check"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
      >
        <path
          class="svg-check__path"
          d="M12 2c5.514 0 10 4.486 10 10s-4.486 10-10 10-10-4.486-10-10 4.486-10 10-10zm0-2c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12zm6.25 8.891l-1.421-1.409-6.105 6.218-3.078-2.937-1.396 1.436 4.5 4.319 7.5-7.627z"
        />
      </svg>
    </div>
    <div class="task__checkbox" v-else @click="toggleCompleted(index)">
      <svg
        class="svg-check"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
      >
        <path
          class="svg-check__path"
          d="M12 2c5.514 0 10 4.486 10 10s-4.486 10-10 10-10-4.486-10-10 4.486-10 10-10zm0-2c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12z"
        />
      </svg>
    </div>
    <input
      class="task__input"
      @keyup.13="editTask(index)"
      type="text"
      v-model="newText"
    />
    <div class="task__tools">
      <button class="task__button" @click="editTask(index)">edit</button>
    </div>
  </div>
  <div class="task" v-else>
    <div class="task__checkbox" v-if="checked" @click="toggleCompleted(index)">
      <svg
        class="svg-check"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
      >
        <path
          class="svg-check__path"
          d="M12 2c5.514 0 10 4.486 10 10s-4.486 10-10 10-10-4.486-10-10 4.486-10 10-10zm0-2c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12zm6.25 8.891l-1.421-1.409-6.105 6.218-3.078-2.937-1.396 1.436 4.5 4.319 7.5-7.627z"
        />
      </svg>
    </div>
    <div class="task__checkbox" v-else @click="toggleCompleted(index)">
      <svg
        class="svg-check"
        xmlns="http://www.w3.org/2000/svg"
        width="24"
        height="24"
        viewBox="0 0 24 24"
      >
        <path
          class="svg-check__path"
          d="M12 2c5.514 0 10 4.486 10 10s-4.486 10-10 10-10-4.486-10-10 4.486-10 10-10zm0-2c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12z"
        />
      </svg>
    </div>
    <div class="task__text">{{ text }}</div>
    <div class="task__tools">
      <button class="task__button" @click="setEditing(index)">edit</button>
      <button class="task__button" @click="removeTask(index)">delete</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    index: Number,
    text: String,
    checked: Boolean,
    onToggleCompeted: Function,
    onRemoveTask: Function,
    onEditTask: Function,
  },
  data: () => ({
    isEditing: false,
    newText: "",
  }),
  methods: {
    toggleCompleted(index) {
      this.$emit("onToggleCompleted", index);
    },
    removeTask(index) {
      this.$emit("onRemoveTask", index);
    },
    setEditing() {
      this.isEditing = true;
    },
    editTask(index) {
      this.$emit("onEditTask", index, this.newText);
      this.isEditing = false;
    },
  },
};
</script>

<style>
.task {
  display: flex;
  margin: 10px;
}
.task__checkbox {
  cursor: pointer;
  padding-right: 10px;
}
.task__tools {
  display: flex;
  margin-left: auto;
}
.task__button {
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  background-color: transparent;
  width: 65px;
  cursor: pointer;
  color: transparent;
}
.task__button:focus {
  outline: none;
}
.task:hover .task__button {
  color: #49d290;
}
.task__button:hover {
  background-color: #fff;
}
.svg-check__path {
  fill: #72ecac;
}
.task__checkbox:hover .svg-check__path {
  fill: #49d290;
}
.task__input {
  outline: none;
  border: none;
  flex: 1;
  background: transparent;
}
.task__input:focus {
  background: #fff;
  border: 2px solid #a4f6cf;
}
.task__input:hover {
  background: #fff;
  border: 2px solid #a4f6cf;
}
</style>