<script setup lang="ts">
import type { Task } from '~/types'
import { nanoid } from 'nanoid'

const emit = defineEmits<{
  (e: 'added', payload: Task) : void
}>()

const isFocused = ref(false)
const title = ref('')

const addTask = (event: Event) => {
  if (title.value.trim()) {
    event.preventDefault()
    emit('added', {
      id: nanoid(),
      title: title.value.trim(),
      createdAt: new Date(),
    } as Task)
  }
  title.value = ''
}
</script>

<template>
  <div>
    <textarea
      v-model="title"
      :placeholder="isFocused ? 'Enter a title for this task' : '+ Add a task'"
      class="focus:bg-white focus:shadow resize-none rouned w-full border-none rounded bg-transparent p-2 cursor-pointer text-sm duration-500 overflow-hidden"
      :class="{
        'h-7': !isFocused,
        'h-20': isFocused,
      }"
      style="outline: none !important;"
      @focus="isFocused = true"
      @blur="isFocused = false"
      @keydown.tab="addTask"
      @keyup.enter="addTask"
    />
  </div>
</template>