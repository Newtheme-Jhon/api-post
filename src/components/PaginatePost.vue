<script setup>

const props = defineProps(['inicio', 'fin', 'maxLength']);
const emit = defineEmits(['next', 'prev']);

</script>

<template>

  <div class="btn-group" role="group" aria-label="Basic example">
    <button type="button" class="btn btn-primary fs-5 fw-semibold px-4 bold" @click="emit('prev')" :disabled="inicio <= 0">
      Previus </button>
    <button type="button" class="btn btn-primary fs-5 fw-semibold px-4 bold" @click="emit('next')" :disabled="fin >= maxLength">
      Next </button>
  </div>

</template>