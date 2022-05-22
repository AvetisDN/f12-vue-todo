<script setup>
import { ref } from "vue";

const todos = ref([
  {
    title: "Learn HTML",
    completed: true,
  },
  {
    title: "Learn CSS",
    completed: true,
  },
  {
    title: "Learn JS",
    completed: false,
  },
]);

const newTodo = ref("");
const modal = ref(false);
const toDelete = ref(-1);

const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
  });
  newTodo.value = "";
};
const deleteTodo = (index) => {
  modal.value = true;
  toDelete.value = index;
};
const removeTodo = () => {
  todos.value.splice(toDelete.value, 1);
  toDelete.value = -1;
  modal.value = false;
};
const completeTodo = (index) => {
  todos.value[index].completed = !todos.value[index].completed;
};
</script>

<template>
  <div class="w-full bg-base-300 min-h-screen flex items-center justify-center">
    <div
      class="w-full max-w-md bg-base-100 p-6 rounded-lg shadow-lg flex flex-col gap-4"
    >
      <h1 class="text-primary text-xl font-black text-center">Todo APP</h1>
      <div class="divider my-0"></div>
      <div class="flex">
        <input
          type="text"
          class="input input-bordered border-r-0 rounded-r-none flex-grow"
          placeholder="Set new todo..."
          v-model="newTodo"
        />
        <button
          class="btn btn-primary rounded-l-none"
          :disabled="newTodo.length < 3"
          @click="addTodo"
        >
          ADD
        </button>
      </div>
      <div class="divider my-0"></div>
      <ul v-if="todos.length">
        <li
          class="flex items-center justify-between bg-base-200 px-3 py-2 rounded-md mb-2"
          v-for="(todo, index) in todos"
        >
          <span
            class="text-lg font-semibold"
            :class="{
              'text-secondary': todo.completed,
              italic: todo.completed,
            }"
          >
            {{ todo.title }}
          </span>
          <div class="flex gap-3 items-center">
            <input
              type="checkbox"
              class="toggle toggle-secondary"
              :checked="todo.completed"
              @change="completeTodo(index)"
            />
            <button
              class="btn btn-sm btn-circle btn-error"
              @click="deleteTodo(index)"
            >
              <i class="fas fa-trash"></i>
            </button>
          </div>
        </li>
      </ul>
      <p v-else>No todos yet...</p>
    </div>
    <div
      class="w-full fixed h-screen bg-black bg-opacity-70 z-50 flex items-center justify-center"
      v-if="modal"
    >
      <div class="fixed z-10 w-full h-full" @click="modal = false"></div>
      <div
        class="bg-base-200 p-6 rounded-lg flex flex-col gap-4 text-center relative z-20"
      >
        <h3 class="text-xl">Are you sure you want to delete this?</h3>
        <div class="flex justify-center gap-3">
          <button class="btn btn-error" @click="removeTodo">Delete</button>
          <button class="btn" @click="modal = false">Cancel</button>
        </div>
      </div>
    </div>
  </div>
</template>
