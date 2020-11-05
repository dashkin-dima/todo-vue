<template>
  <div class="task-field">
    <input
      class="task-field__input"
      @keyup.13="addTask"
      v-model="text"
      placeholder="enter"
    />
    <button class="task-field__button" @click="addTask">
      <svg
        class="task-field__svg-add svg-add"
        width="14px"
        height="14px"
        viewBox="0 0 14 14"
        version="1.1"
        xmlns="http://www.w3.org/2000/svg"
        xmlns:xlink="http://www.w3.org/1999/xlink"
      >
        <g
          id="Icons"
          stroke="none"
          stroke-width="1"
          fill="none"
          fill-rule="evenodd"
        >
          <g id="Rounded" transform="translate(-411.000000, -1487.000000)">
            <g id="Content" transform="translate(100.000000, 1428.000000)">
              <g
                id="-Round-/-Content-/-add"
                transform="translate(306.000000, 54.000000)"
              >
                <g transform="translate(0.000000, 0.000000)">
                  <polygon id="Path" points="0 0 24 0 24 24 0 24"></polygon>
                  <path
                    class="svg-add__path"
                    d="M18,13 L13,13 L13,18 C13,18.55 12.55,19 12,19 C11.45,19 11,18.55 11,18 L11,13 L6,13 C5.45,13 5,12.55 5,12 C5,11.45 5.45,11 6,11 L11,11 L11,6 C11,5.45 11.45,5 12,5 C12.55,5 13,5.45 13,6 L13,11 L18,11 C18.55,11 19,11.45 19,12 C19,12.55 18.55,13 18,13 Z"
                    id="🔹Icon-Color"
                    fill="#1D1D1D"
                  ></path>
                </g>
              </g>
            </g>
          </g>
        </g>
      </svg>
    </button>
  </div>
</template>

<script>
export default {
  name: "TaskField",
  props: {
    onAddTask: Function,
  },
  data: () => ({
    text: "",
  }),
  methods: {
    addTask() {
      if (this.text) {
        this.$emit("onAddTask", this.text);
        this.text = "";
      } else {
        alert("enter text");
      }
    },
  },
};
</script>

<style scoped>
.task-field {
  display: flex;
  border-top: 1px solid #49d290;
}
.task-field__input {
  outline: none;
  border: none;
  font-size: 18px;
  padding: 20px;
  flex: 1;
  background: transparent;
}
.task-field__input:focus {
  background: #fff;
  border: 2px solid #a4f6cf;
}
.task-field__input:hover {
  background: #fff;
  border: 2px solid #a4f6cf;
}
.task-field__button {
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  background-color: transparent;
  width: 65px;
  cursor: pointer;
}
.task-field__button:focus {
  outline: none;
}
.task-field__button:hover {
  background-color: #fff;
}
.svg-add__path {
  fill: #72ecac;
}
.task-field__button:hover .svg-add__path {
  fill: #49d290;
}
</style>