<script setup>
defineProps(["newTodo"]);
defineEmits(["add-todo"]);
</script>

<template>
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
      @click="
        () => {
          $emit('add-todo', newTodo);
          newTodo = '';
        }
      "
    >
      ADD
    </button>
  </div>
</template>
