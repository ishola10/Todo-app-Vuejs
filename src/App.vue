<template>
  <div class="todo-app">
    <h1>Todo App</h1>

    <div class="input-container">
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="Add new todo"
      />
      <button @click="addTodo">Add</button>
    </div>

    <ul class="todos">
      <li v-for="(todo, index) in todos" :key="index">
        <div v-if="!todo.editing">{{ todo.text }}</div>
        <div v-else>
          <input v-model="todo.text" @keyup.enter="saveEdit(todo)" />
          <button @click="saveEdit(todo)">Save</button>
        </div>
        <div>
          <button @click="toggleEdit(todo)">Edit</button>
          <button @click="deleteTodo(index)">
            <svg
              class="delete-button"
              xmlns="http://www.w3.org/2000/svg"
              x="0px"
              y="0px"
              width="40"
              height="15"
              viewBox="0 0 24 24"
            >
              <path d="M3 3H21V5H3z"></path>
              <path
                d="M16.1,22H7.9c-1,0-1.9-0.7-2-1.7L4,4.1l2-0.2L7.9,20l8.2,0L18,3.9l2,0.2l-1.9,16.1C18,21.3,17.1,22,16.1,22z"
              ></path>
              <path
                d="M5,4l1.9,16.1c0.1,0.5,0.5,0.9,1,0.9h8.2 c0.5,0,0.9-0.4,1-0.9L19,4H5z"
                opacity=".3"
              ></path>
              <path d="M15 3L15 4 9 4 9 3 10 2 14 2z"></path>
            </svg>
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: [],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() !== '') {
        this.todos.push({ text: this.newTodo, editing: false });
        this.newTodo = '';
      }
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
    },
    toggleEdit(todo) {
      todo.editing = !todo.editing;
    },
    saveEdit(todo) {
      todo.editing = false;
    },
  },
};
</script>

<style scoped>
.todo-app {
  font-family: Arial, sans-serif;
  max-width: 400px;
  margin: 0 auto;
}

.input-container {
  margin-bottom: 10px;
  gap: 10px;
  display: flex;
}

.todos {
  list-style: none;
  padding: 0;
}

.todos li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5px;
}

.todos li input {
  width: 150px;
}

.todos li button {
  margin-left: 5px;
}
</style>
