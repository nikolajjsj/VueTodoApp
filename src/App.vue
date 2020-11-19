<template>
  <h1>Vue Todo App</h1>
  <form @submit.prevent="addNewTodo">
    <label for="newTodo">New Todo</label>
    <input v-model="newTodo" name="newTodo" />
    <button>Add New Todo</button>
  </form>
  <button v-if="todos.length > 0" @click="markAllDone">Mark All Done</button>
  <button v-if="todos.length > 0" @click="removeAllTodos">Remove All</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{ todo.content + " - " }}
        <strong @click="removeTodo(index)">X</strong>
      </h3>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      // eslint-disable-next-line no-param-reassign
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    }

    function markAllDone() {
      todos.value.forEach((todo) => {
        // eslint-disable-next-line no-param-reassign
        todo.done = true;
      });
    }

    function removeAllTodos() {
      todos.value = [];
    }

    return {
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}

input,
textarea,
button,
p,
div,
section,
section,
article,
select {
  display: block;
  width: 100%;
  font-size: 1em;
  margin: 0.5em;
  box-sizing:border-box
}

.done {
  text-decoration: line-through;
}

.todo {
  cursor: pointer;
}
</style>
