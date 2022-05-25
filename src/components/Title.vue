<script setup>
defineProps(["title", "icon"]);
</script>

<template>
  <h1
    class="text-primary text-xl font-black text-center flex gap-3 justify-center items-center"
  >
    <i class="fas text-4xl -translate-y-1" :class="`fa-${icon}`"></i>
    {{ title }}
  </h1>
</template>
