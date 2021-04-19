<template>
  <button @click="openForm" v-show="!isCreating">Add NewTodo</button>

  <section v-show="isCreating">
    <header><h1>Add To-Do</h1></header>

    <div class="form-control" @submit.prevent="addTodo()">
      <label for="title">Title</label>
      <input
        id="title"
        type="search"
        v-model="enteredTodoTitle"
        placeholder="What need to be done?"
      /><br />
      <label for="description">Description</label>
      <textarea
        id="description"
        name="description"
        v-model="enteredTodoDesc"
        rows="3"
      ></textarea
      ><br />
      <label for="status">status</label>
      <input
        id="title"
        type="search"
        v-model="enteredTodoStatus"
        placeholder="What need to be done?"
      /><br />
      <button type="submit" @click="sendForm">Submit</button>
      <button @click="closeForm">Cancel</button>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      enteredTodoTitle: "",
      enteredTodoDesc: "",
      enteredTodoStatus: "",
      isCreating: false,
    };
  },
  emits:['new-todo'],  //Defining custom Event
  methods: {
    openForm() {
      this.isCreating = true;
    },
    closeForm() {
      this.isCreating = false;
    },
    sendForm() {
      if (this.enteredTodoTitle.length > 0 && this.enteredTodoDesc.length > 0) {
        const title = this.enteredTodoTitle;
        const description = this.enteredTodoDesc;
        const status = this.enteredTodoStatus;

        this.$emit("new-todo", {
          title,
          description,
          status,
          done: false,
        });
        this.enteredTodoTitle = "";
        this.enteredTodoDesc = "";
        this.enteredTodoStatus=" ";
        this.isCreating = false;
      }
    },
  },
};
</script>
<style scoped>
input {
  display: block;
  width: 100%;
  height: 30px;
  font: inherit;
  margin-top: 0.5rem;
}
header {
  width: 100%;
  height: 5rem;
  background-color: hsl(12, 28%, 46%);
  display: flex;
  justify-content: center;
  align-items: center;
}

header h1 {
  color: white;
  margin: 0;
}
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: hsl(13, 30%, 51%);
  border: 1px solid hsl(12, 28%, 46%);
  color: white;
  cursor: pointer;
  margin-left: 0.5rem;
}

button:hover,
button:active {
  background-color: hsl(12, 28%, 46%);
  border-color: hsl(12, 28%, 46%);
}
</style>
