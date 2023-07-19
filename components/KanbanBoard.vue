<script setup lang="ts">
import type { Column } from '~/types'
import draggable from 'vuedraggable'
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
  <div>
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      :animation="300"
      handle=".drag-icon"
      class="flex items-start gap-4 overflow-x-auto"
    >
    <template #item="{ element: col }: { element: Column }">
      <section class="bg-blue-100 p-6 rounded min-w-[240px] mb-8">
        <header class="font-bold mb-4">
          <DragIcon />
          {{ col.title }}
        </header>
        <KanbanBoardTask
          v-for="task in col.tasks"
          :key="task.id"
          :task="task"
        />
        <footer>
          <button class="text-sm text-gray-400 hover:text-gray-600 duration-500">
            + Add a task
          </button>
        </footer>
      </section>
    </template>
    </draggable>
  </div>
</template>