<template>
  <div v-if="!pending" class="unload-cards">
    <UnloadListItem v-for="item of items" :key="item.id" :item="item" @click="$emit('show-info', item)" />
  </div>
  <div v-else-if="error">
    {{ error?.message }}
  </div>
  <div v-else>
    Загрузка...
  </div>
</template>

<script setup>
import {  computed } from 'vue';

defineEmits(['show-info']);

const { data, pending, error } = await useAPIFetch('e.scripts?page=pages:unload&event=get');

const items = computed(() => {
  return JSON.parse(data.value).response.data
});

</script>
