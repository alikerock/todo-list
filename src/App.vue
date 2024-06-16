<script setup>
import { ref, reactive } from 'vue'
import Todo from './components/TodoItem.vue'

// 상태 변수와 함수 정의
const todoText = ref('')
const todos = reactive([
  { id: 1, text: 'learn web', checked: false },
  { id: 2, text: 'get a job', checked: false },
])

// 할 일 추가 함수 정의
function addTodo() {
  if (todoText.value.trim()) {
    todos.push({
      id: todos.length + 1,
      text: todoText.value,
      checked: false
    })
    todoText.value = ''
  }
}
// 체크 업데이트
function toggleCheckbox({ id, checked }) {
  const index = todos.findIndex(todo => {
    return todo.id === id;
  });
  todos[index].checked = checked;
}
// 삭제
function deletetodo(id) {
  if (window.confirm('정말 삭제할까요')) {
    const index = todos.findIndex(todo => {
      return todo.id === id;
    });
    todos.splice(index, 1);
  }
}

</script>

<template>
  <div class="container">
    <h1 class="text-center">Todo App</h1>
    <input v-model="todoText" type="text" class="w-100 p-2" placeholder="할일을 입력하세요" @keyup.enter="addTodo">
    <hr>
    <Todo v-for="todo in todos" :key="todo.id" :todo="todo" @toggle-checkbox="toggleCheckbox"
      @click-delete="deletetodo"></Todo>

  </div>
</template>

<style scoped></style>
