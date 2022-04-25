<script setup>
import { ref, computed } from 'vue';

const todos = ref([]);

const activeTodos = computed(() => {
  return todos.value.filter((todo) => !todo.completed).length;
});
function addTodo(e) {
  const value = e.target.value.trim();
  if (value) {
    todos.value.push({
      id: Date.now(),
      title: value,
      completed: false,
    });
    e.target.value = '';
  }
}
function removeTodo(todo) {
  // console.log(todo)
  // console.log(todos.value[0].id)
  // todos.value.splice(todos.value.indexOf(todo), 1)
  todos.value = todos.value.filter((_todo) => _todo.id !== todo.id);
}
</script>

<template>
  <section class="todoapp">
    <header>
      <h1>todos</h1>
    </header>
    <input
      type="text"
      class="new-todo"
      autofocus
      placeholder="需要做什麼？"
      @keyup.enter="addTodo"
    />
    <main class="main" v-show="todos.length !== 0">
      <input id="toggle-all" type="checkbox" class="toggle-all" />
      <label for="toggle-all"></label>
      <ul class="todo-list">
        <li
          v-for="todo in todos"
          :key="todo.id"
          class="todo"
          :class="{ completed: todo.completed }"
        >
          <div class="view">
            <input v-model="todo.completed" type="checkbox" class="toggle" />
            <label for="">{{ todo.title }}</label>
            <button @click="removeTodo(todo)" class="destroy"></button>
          </div>
          <input type="text" class="edit" />
        </li>
      </ul>
    </main>
    <footer class="footer" v-show="todos.length !== 0">
      <span class="todo-count">
        <strong>{{ activeTodos }}</strong>
        items left
      </span>
      <ul class="filters">
        <li>
          <a href="#/all">All</a>
        </li>
        <li>
          <a href="#/active">Active</a>
        </li>
        <li>
          <a href="#/completed">Completed</a>
        </li>
      </ul>
      <button class="clear-completed">Clear completed</button>
    </footer>
  </section>
</template>

<style>
@import 'https://unpkg.com/todomvc-app-css@2.4.1/index.css';
</style>
