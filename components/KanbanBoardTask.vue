<script setup lang="ts">
import type { Task } from '~/types'

defineProps<{
  task: Task
}>()
</script>

<template>
  <div
    :title="task.createdAt.toLocaleDateString"
    class="bg-white p-1 mb-2 rounded shadow-sm max-w-[200px]"
  >
    <span>{{ task.title }}</span>
  </div>
</template>