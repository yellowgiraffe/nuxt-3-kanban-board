<script setup lang="ts">
import type { Task, ID } from '~/types'

const props = defineProps<{
  task: Task
}>()

const emit = defineEmits<{
  (e: 'deleted', payload: ID) : void
}>()

const isFocused = ref(false)
const isExpanded = ref(false)

onKeyStroke('Backspace', (event) => {
  if (isFocused.value) emit('deleted', props.task.id)
})
</script>

<template>
  <div
    :title="task.createdAt.toLocaleString('pl-PL')"
    class="task flex items-start bg-white p-2 mb-2 rounded shadow-sm"
    tabindex="0"
    @focus="isFocused = true"
    @blur="isFocused = false"
  >
    <DragIcon class="mt-1"/>
    <textarea
      v-model="task.title"
      type="text"
      wrap="hard"
      class="text-sm resize-none duration-500 overflow-hidden px-1 ml-1"
      :class="{
        'h-5': !isExpanded,
        'h-10': isExpanded,
      }"
      style="outline: none !important;"
      @focus="isExpanded = true"
      @blur="isExpanded = false"
    />
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
  outline: #bfdbfe auto 1px;
}
</style>