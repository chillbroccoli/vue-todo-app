<template>
  <div class="flex items-center justify-center w-full h-full">
    <div class="w-[95%] lg:w-[550px] h-[550px] lg:h-[650px] p-6">
      <Form @add-todo="addTodo"></Form>

      <div class="h-full mt-6 overflow-y-auto">
        <ul role="list" class="space-y-3">
          <Todo
            v-for="todo in todos"
            :todo="todo"
            :key="todo.id"
            @remove-todo="removeTodo"
          />
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref, watch } from "vue";
import { nanoid } from "nanoid";
import Form from "./components/Form.vue";
import Todo from "./components/Todo.vue";
import type { Todo as TodoType } from "./lib/types";

const todos = ref<TodoType[]>([]);

const addTodo = (text: string) => {
  const newTodo = {
    id: nanoid(),
    text,
    completed: false,
  };

  todos.value = [...todos.value, newTodo];
};

const removeTodo = (id: string) => {
  const updatedTodos = todos.value.filter((todo) => todo.id !== id);
  todos.value = [...updatedTodos];
};

watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  {
    deep: true,
  }
);

onMounted(() => {
  const items = JSON.parse(localStorage.getItem("todos") || "[]");
  todos.value = items;
});
</script>
