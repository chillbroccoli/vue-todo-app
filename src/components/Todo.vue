<template>
  <li
    @mouseover="isHovered = true"
    @mouseout="isHovered = false"
    class="flex items-center justify-between px-6 py-4 overflow-hidden border-2 rounded-md shadow bg-zinc-700 border-indigo-600/30"
  >
    <div class="flex items-center gap-x-2">
      <div class="relative flex items-start">
        <div class="flex items-center h-6">
          <input
            id="completed"
            aria-describedby="completed"
            name="completed"
            type="checkbox"
            v-model="todo.completed"
            class="w-4 h-4 text-indigo-600 rounded bg-zinc-500 focus:ring-indigo-600"
          />
        </div>
      </div>

      <span
        :class="
          clsx(
            'text-zinc-300 text-xs lg:text-sm',
            todo.completed ? 'line-through text-zinc-500' : ''
          )
        "
      >
        {{ todo.text }}
      </span>
    </div>

    <div class="flex items-center justify-center gap-x-1">
      <button
        class="flex items-center justify-center rounded-md bg-rose-600/20 group hover:bg-rose-600/30"
        @click="emit('removeTodo', todo.id)"
      >
        <IconTrash
          :size="24"
          class="p-1 stroke-rose-400 group-hover:stroke-rose-400/90"
        />
      </button>
    </div>
  </li>
</template>

<script setup lang="ts">
import { ref } from "vue";
import clsx from "clsx";
import { IconTrash } from "@tabler/icons-vue";
import { Todo } from "../lib/types";

const { todo } = defineProps<{ todo: Todo }>();
const emit = defineEmits<{
  (name: "removeTodo", id: string): void;
}>();

const isHovered = ref(false);
</script>

<style>
.v-enter-active,
.v-leave-active {
  transition: opacity 0.25s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
