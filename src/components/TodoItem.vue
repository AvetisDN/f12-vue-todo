<script setup>
defineProps(["todo", "index"]);
defineEmits(["complete", "delete"]);
</script>

<template>
  <li
    class="flex items-center justify-between bg-base-200 px-3 py-2 rounded-md mb-2"
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
        @change="$emit('complete', index)"
      />
      <button
        class="btn btn-sm btn-circle btn-error"
        @click="$emit('delete', index)"
      >
        <i class="fas fa-trash"></i>
      </button>
    </div>
  </li>
</template>
