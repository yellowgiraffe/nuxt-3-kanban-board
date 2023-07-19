<script setup lang="ts">
import { Column } from '~/types'
import { nanoid } from 'nanoid'
const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: 'Backlog',
    tasks: [
      {
        id: nanoid(),
        title: 'Send a package to Dawid',
        createdAt: new Date()
      }
    ]
  },
  {
    id: nanoid(),
    title: 'In Progress',
    tasks: [
      {
        id: nanoid(),
        title: 'Do homework',
        createdAt: new Date()
      }
    ]
  },
  {
    id: nanoid(),
    title: 'In Progress',
    tasks: [
      {
        id: nanoid(),
        title: 'Do homework',
        createdAt: new Date()
      },
      {
        id: nanoid(),
        title: 'Do homework',
        createdAt: new Date()
      }
    ]
  },
  {
    id: nanoid(),
    title: 'In Progress',
    tasks: [
      {
        id: nanoid(),
        title: 'Do homework',
        createdAt: new Date()
      }
    ]
  },
  {
    id: nanoid(),
    title: 'In Progress',
    tasks: [
      {
        id: nanoid(),
        title: 'Do homework',
        createdAt: new Date()
      }
    ]
  }
])
</script>

<template>
  <div class="flex items-start gap-4 overflow-x-auto">
    <div
      v-for="col in columns"
      :key="col.id"
      class="bg-blue-100 p-6 rounded min-w-[240px]"
    >
      <header>
        {{ col.title }}
      </header>
      <p v-for="task in col.tasks" :key="task.id">
        {{ task.title }}
      </p>
    </div>
  </div>
</template>