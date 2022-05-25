<script setup>
defineProps(["modal"]);
defineEmits(["remove", "close-modal"]);
</script>

<template>
  <div
    class="w-full fixed h-screen bg-black bg-opacity-70 z-50 flex items-center justify-center"
  >
    <div class="fixed z-10 w-full h-full" @click="$emit('close-modal')"></div>
    <div
      class="bg-base-200 p-6 rounded-lg flex flex-col gap-4 text-center relative z-20"
    >
      <h3 class="text-xl">Are you sure you want to delete this?</h3>
      <div class="flex justify-center gap-3">
        <button class="btn btn-error" @click="$emit('remove')">Delete</button>
        <button class="btn" @click="$emit('close-modal')">Cancel</button>
      </div>
    </div>
  </div>
</template>
