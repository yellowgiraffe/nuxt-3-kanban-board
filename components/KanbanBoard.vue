<script setup lang="ts">
import type { Column, Task } from '~/types'
import draggable from 'vuedraggable'
import { nanoid } from 'nanoid'
const columns = ref<Column[]>([
  {
    id: nanoid(),
    title: 'Backlog',
    tasks: [
      {
        id: nanoid(),
        title: 'Send a package to Dawid fend a package to Dawid',
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
const ctrl = useKeyModifier('Control')
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
    <template #item="{ element: col } : { element: Column }">
      <section class="bg-blue-100 p-6 rounded min-w-[240px] mb-8">
        <header class="font-bold mb-4">
          <DragIcon />
          {{ col.title }}
        </header>
        <draggable
          v-model="col.tasks"
          :group="{ name: 'tasks', pull: ctrl ? 'clone' : true }"
          item-key="id"
          handle=".drag-icon"
          :animation="300"
        >
          <template #item="{ element: task } : { element: Task }">
            <KanbanBoardTask
              :task="task"
              @deleted="col.tasks = col.tasks.filter(el => el.id !== $event)"
            />
          </template>
        </draggable>
        <footer>
          <!-- <button class="text-sm text-gray-400 hover:text-gray-600 duration-500">
            + Add a task
          </button> -->
          <NewTask @added="col.tasks.push($event)"/>
        </footer>
      </section>
    </template>
    </draggable>
  </div>
</template>