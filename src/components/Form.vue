<template>
  <div>
    <div class="mt-2">
      <form @submit.prevent="handleSubmit">
        <input
          type="text"
          name="text"
          id="text"
          v-model="text"
          class="block w-full px-6 py-4 text-gray-300 border-0 rounded-md shadow-sm bg-zinc-700 ring-1 ring-inset ring-zinc-500 placeholder:text-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Add todo..."
        />
      </form>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits<{ (name: "addTodo", text: string): void }>();

const text = ref("");

const handleSubmit = () => {
  if (!text.value) {
    alert("Cannot add empty todo");
    return;
  }

  emit("addTodo", text.value);

  text.value = "";
};
</script>
