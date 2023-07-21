<script setup lang="ts">
import type { Column, Task } from '~/types'
import draggable from 'vuedraggable'
import { nanoid } from 'nanoid'
const columns = useLocalStorage<Column[]>('boardData', [
  {
    id: nanoid(),
    title: 'Backlog',
    tasks: [
      {
        id: nanoid(),
        title: 'Send a package',
        createdAt: new Date()
      },
      {
        id: nanoid(),
        title: 'Make presentation',
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
        title: 'Deploy website',
        createdAt: new Date()
      }
    ]
  },
])
const ctrl = useKeyModifier('Control')

const addColumn = () => {
  const col: Column = {
    id: nanoid(),
    title: '',
    tasks: []
  }

  columns.value.push(col)
  nextTick(() => {
    (
      document.querySelector(
        '.column:last-of-type .column-title'
        ) as HTMLInputElement
    ).focus()
  })
}
</script>

<template>
  <div class="flex items-start gap-4 overflow-x-auto">
    <draggable
      v-model="columns"
      group="columns"
      item-key="id"
      :animation="300"
      handle=".drag-icon"
      class="flex items-start gap-4"
    >
    <template #item="{ element: col } : { element: Column }">
      <section class="column bg-blue-100 px-6 pt-2 pb-6 rounded min-w-[255px] mb-28">
        <header class="font-bold mb-4">
          <div class="text-right mb-1 mr-2">
            <button
              class="text-xs text-gray-400 hover:text-rose-500 duration-500"
              @click="columns = columns.filter(el => el.id !== col.id)"
            >
              ✕
            </button>
          </div>
          <DragIcon class="m-2" />
          <input
            v-model="col.title"
            type="text"
            :placeholder="!col.title ? 'Enter a title' : ''"
            class="column-title bg-transparent focus:bg-white w-44 outline-blue-200 px-1 duration-500 mr-1 placeholder:text-sm placeholder:font-normal"
            @keyup.enter="($event.target as HTMLInputElement).blur()"
          />
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
          <NewTask @added="col.tasks.push($event)"/>
        </footer>
      </section>
    </template>
    </draggable>
    <button
      class="bg-blue-100 p-2 text-sm whitespace-nowrap rounded opacity-50 hover:opacity-80 duration-500 min-w-[240px]"
      @click="addColumn"
    >
      + Add a column
    </button>
  </div>
</template>