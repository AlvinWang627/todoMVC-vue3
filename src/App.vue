<script setup>
import { ref } from 'vue'
const todos = ref([
  {
    title: '學習 Vue Template 的使用',
    completed: true,
  },
  {
    title: '學習在 Vue Template 中進行條件判斷',
    completed: false,
  },
  {
    title: '學習在 Vue Template 中使用迴圈',
    completed: false,
  }
])
</script>


<template>
  <section class="todoapp">
    <header>
      <h1>todos</h1>
    </header>
    <input type="text" class="new-todo" autofocus placeholder="需要做什麼？" />
    <main class="main">
      <input id="toggle-all" type="checkbox" class="toggle-all" />
      <label for="toggle-all"></label>
      <ul class="todo-list">
        <li v-for="todo in todos" class="todo" :class="{ completed: todo.completed }">
          <div class="view">
            <input type="checkbox" class="toggle" />
            <label for="">{{ todo.title }}</label>
            <button class="destroy"></button>
          </div>
          <input type="text" class="edit" />
        </li>
      </ul>
    </main>
    <footer class="footer">
      <span class="todo-count"> <strong>3</strong> items left </span>
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
