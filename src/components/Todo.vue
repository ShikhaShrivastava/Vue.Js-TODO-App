<template>
  <!--Diplay Dummy Data -->
  <section>
    <div v-if="!isEditing">
      <div class="header">{{ title }}</div>
      <div class="meta">{{ description }}</div>
      <div class="">{{ status }}</div>
      <br />
      <button @click="isEditing = true">
        <span>Edit</span>
      </button>
      <button @click="$emit('on-delete')">Delete</button>
    </div>

    <!--EDITING PART-->
    <div class="form-control" v-else >
      <label for="title">Title</label>
      <input
        id="title"
        type="search"
        ref="enteredTodoTitle"
        v-model="newTodoTitle"
        placeholder="What need to be done?"
      /><br />
      <label for="description">Description</label>
      <textarea
        id="description"
        name="description"
        v-model="newTodoDescription"
        ref="enteredTodoDesc"
        rows="3"
      ></textarea>
      <label for="status">status</label>
      <input
        id="status"
        type="text"
        v-model="newTodoStatus"
        placeholder="Enter status"
        ref="enteredTodoStatus"
      />
      <button @click="isEditing = false">Close</button>
      <button @click="finishEditing()">Save</button>
    </div>

    <br />
   
  </section>
</template>
<script>
export default {
  props: {
    title: String,
    description: String,
    status: String,
    completed: Boolean,
    index: Number
  },
  data() {
    return {
      isEditing: false,
      newTodoTitle:'',
      newTodoDescription:'',
      newTodoStatus:'',
    };
  },
  mounted () {
    this.newTodoTitle = this.title;
    this.newTodoDescription = this.description;
    this.newTodoStatus = this.status; 
  },
  methods: {
    finishEditing() {
      this.isEditing = false
      this.$emit(
        "on-edit",
        { title:this.newTodoTitle,
        description: this.newTodoDescription,
        status:this.newTodoStatus, index: this.index}
      );
    },
  },
};
</script>
<style>
button {
  padding: 0.75rem 1.5rem;
  font-family: inherit;
  background-color: #3a0061;
  border: 1px solid #3a0061;
  color: white;
  cursor: pointer;
  margin-left: 0.5rem;
}

button:hover,
button:active {
  background-color: #270041;
  border-color: #270041;
}
.form-control {
  margin: 1rem 0;
}
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
  text-align: start;
}
textarea {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
  display: block;
  width: 100%;
  height: 25%;
}
section {
  padding: 1rem;
  margin: 1rem auto;
}
</style>
