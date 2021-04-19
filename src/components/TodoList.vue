<template>
    <base-card>
      <header><h2>Status</h2></header>
      <p>
        <strong class="pending"> Pending Todo's:</strong>
        {{
          todos.filter((todo) => {
            return todo.done === true;
          }).length
        }}
      </p>
      <p>
        <strong class="Done"> Done Todo's:</strong>
        {{
          todos.filter((todo) => {
            return todo.done === false;
          }).length
        }}
      </p>
    </base-card>
    <base-card>
      <header><h2>Todo's</h2></header>

      <todo
        v-for="(todo, index) in todos"
        :key="index"
        :title="todo.title"
        :description="todo.description"
        :status="todo.status"
        :completed="todo.completed"
        @on-toggle="toggleTodo(todo)"
        @on-delete="deleteTodo(todo)"
        @on-edit="editTodo(todo, $event)"
      />
    </base-card>
  <new-todo @new-todo="newTodoList" />
</template>

<script>
import Todo from "./Todo.vue";
import NewTodo from "./NewTodo.vue";
import BaseCard from "./UI/BaseCard.vue";
export default {
  name: "App",
  components: {
    Todo,
    NewTodo,
    BaseCard,
  },
  data() {
    return {
      todos: [
        {
          title: "Learn Vue.js",
          description:
            "Need to practice Rendering list and practical implementation ",
          status: "Done",
          done: false,
        },
        {
          title: "Reading Book",
          description: "Continue Reading Think & Grow Rich ",
          status: "Done",
          done: false,
        },
        {
          title: "Dancing",
          description: "Have to create one more videos for youtube",
          status: "Pending",
          done: true,
        },
      ],
    };
  },
  methods: {
    addTodo(todos) {
      this.todos.push({ ...todos, done: false });
    },
    toggleTodo(todo) {
      todo.done = !todo.done;
    },
    deleteTodo(deletedTodo) {
      this.todos = this.todos.filter((todo) => todo !== deletedTodo);
    },
    editTodo(todo, newTodoTitle, newTodoDescription, newTodoStatus) {
      todo.title = newTodoTitle;
      todo.description = newTodoDescription;
      todo.status = newTodoStatus;
    },
    newTodoList(newTodo) {
      this.todos.push(newTodo);
    },
  
  },
};
</script>
<style scoped>
header {
  width: 100%;
  height: 2rem;
  background-color: hsl(100, 3%, 43%);
  display: flex;
  justify-content: center;
  align-items: center;
}

header h2 {
  color: white;
  margin: 0;
}
section {
  background-color: rgba(240, 240, 240, 0.959);
}
.pending {
  color: red;
}
.Done {
  color: green;
  font-style: italic;
}
</style>
