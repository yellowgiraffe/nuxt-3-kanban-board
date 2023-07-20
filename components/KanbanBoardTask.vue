<script setup lang="ts">
import type { Task } from '~/types'

defineProps<{
  task: Task
}>()
</script>

<template>
  <div
    :title="task.createdAt.toLocaleDateString()"
    class="bg-white py-1 pr-1 mb-2 rounded shadow-sm max-w-[200px]"
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
</style>