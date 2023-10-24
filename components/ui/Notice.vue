<template>
  <div class="notice" :data-color="color">
    <slot name="default" />
  </div>
</template>

<script setup>
defineProps({
  color: {
    type: String,
    default: 'light-purple',
    validator: (v) => ['light-purple', 'yellow', 'gray', 'purple', 'orange', 'red', 'black', 'blue', 'light-blue', 'very-light-blue', 'green', 'white', 'tinkoff'].includes(v),
  },
});
</script>
