<script setup>
import { ref, computed } from 'vue';

const todos = ref([]);
const visibility = ref('all');
const STORAGE_KEY = 'todomvc-app-vue'
const filters = {
  all: (todos) => todos,
  active: (todos) => todos.filter((todo) => !todo.completed),
  completed: (todos) => todos.filter((todo) => todo.completed),
};

function setVisibility(vs) {
  console.log(todos.value);
  visibility.value = vs;
}
const filteredTodos = computed(() => {
  return filters[visibility.value](todos.value);
});
const remaining = computed(() => {
  return filters.active(todos.value).length;
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
  // todos.value.splice(todos.value.indexOf(todo), 1)
  todos.value = todos.value.filter((_todo) => _todo.id !== todo.id);
}

function removeCompleted() {
  todos.value = filters.active(todos.value);
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
          v-for="todo in filteredTodos"
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
        <strong>{{ remaining }}</strong>
        {{ remaining === 1 ? 'item' : 'items' }} left
      </span>
      <ul class="filters">
        <li>
          <a
            href="#/all"
            @click="setVisibility('all')"
            :class="{ selected: visibility === 'all' }"
            >All</a
          >
        </li>
        <li>
          <a
            href="#/active"
            @click="setVisibility('active')"
            :class="{ selected: visibility === 'active' }"
            >Active</a
          >
        </li>
        <li>
          <a
            href="#/completed"
            @click="setVisibility('completed')"
            :class="{ selected: visibility === 'completed' }"
            >Completed</a
          >
        </li>
      </ul>
      <button
        class="clear-completed"
        @click="removeCompleted"
        v-show="todos.length > remaining"
      >
        Clear completed
      </button>
    </footer>
  </section>
</template>

<style>
@import 'https://unpkg.com/todomvc-app-css@2.4.1/index.css';
</style>
