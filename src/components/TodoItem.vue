<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  todo: {
    type: Object,
    required: true
  }
})
//할일 체크 업데이트

const emit = defineEmits(['toggle-checkbox'])

function toggleCheckbox(e) {
  console.log('checked')
  emit('toggle-checkbox', {
    id: props.todo.id,
    checked: e.target.checked
  })
}
//할일 삭제
function clickDelete() {
  emit('click-delete', props.todo.id);
}
</script>

<template>
  <div class="m-3">
    <input type="checkbox" :checked="todo.checked" @change="toggleCheckbox">
    <span class="ml-3 flex-grow-1" :class="todo.checked ? 'text-muted' : ''"
      :style="todo.checked ? 'text-decoration:line-through' : ''">
      {{ todo.text }}
    </span>
    <button class="btn btn-danger btn-sm" @click="clickDelete">Delete</button>
  </div>
</template>
