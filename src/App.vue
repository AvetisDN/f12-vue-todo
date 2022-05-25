<script setup>
import { ref } from "vue";
import Title from "./components/Title.vue";
import TodoItem from "./components/TodoItem.vue";
import AddTodo from "./components/AddTodo.vue";
import Modal from "./components/Modal.vue";
import Layout from "./components/Layout.vue";

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

const closeModal = () => {
  modal.value = false;
};
const addTodo = (str) => {
  todos.value.push({
    title: str,
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
  <Layout>
    <div
      class="w-full max-w-md bg-base-100 p-6 rounded-lg shadow-lg flex flex-col gap-4"
    >
      <!-- Title Component -->
      <Title title="Todo APP" icon="calendar-check" />
      <div class="divider my-0"></div>
      <!-- Add Todo Form Component -->
      <AddTodo :newTodo="newTodo" @add-todo="(str) => addTodo(str)" />
      <div class="divider my-0"></div>
      <ul v-if="todos.length">
        <!-- Loop of Todo Items -->
        <TodoItem
          v-for="(todo, index) in todos"
          :key="index"
          :todo="todo"
          :index="index"
          @complete="(id) => completeTodo(id)"
          @delete="(id) => deleteTodo(id)"
        />
      </ul>
      <p v-else>No todos yet...</p>
    </div>
    <!-- Modal -->
    <Modal
      v-if="modal"
      :modal="modal"
      @remove="removeTodo"
      @close-modal="closeModal"
    />
  </Layout>
</template>
