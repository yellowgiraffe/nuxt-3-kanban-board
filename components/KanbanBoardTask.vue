<script setup lang="ts">
import type { Task, ID } from '~/types'

const props = defineProps<{
  task: Task
}>()

const emit = defineEmits<{
  (e: 'deleted', payload: ID) : void
}>()

const isFocused = ref(false)

onKeyStroke('Backspace', (event) => {
  if (isFocused.value) emit('deleted', props.task.id)
})
</script>

<template>
  <div
    :title="task.createdAt.toLocaleString()"
    class="task bg-white py-1 pr-1 mb-2 rounded shadow-sm max-w-[200px]"
    tabindex="0"
    @focus="isFocused = true"
    @blur="isFocused = false"
  >
    <DragIcon />
    <span class="text-sm">{{ task.title }}</span>
  </div>
</template>

<style>
.sortable-ghost img {
  display: none !important;
}

.sortable-ghost {
  background-color: #c3ccdf;
  color: #c3ccdf;
}

.task:focus,
.task:focus-visible {
  /* @apply outline-gray-400 !important; */
  outline: #c7d5fd auto 1px;
}
</style>