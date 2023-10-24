<template>
  <button type="button" class="unload-card block" :class="{'unload-card--success': item.status === 'green', 'unload-card--danger': item.status === 'red'}">
    <span class="unload-card__row" v-html="DOMPurify.sanitize(item.task_date)" />
    <span class="unload-card__row">
      Статус задачи: <span class="text-bold">{{ item.status_text }}</span>
    </span>
    <span class="unload-card__row">
      ID выгрузки: <span class="text-bold">{{ item.id }}</span>
    </span>
    <span class="unload-card__row" v-html="DOMPurify.sanitize(item.event)" />
    <span class="unload-card__row">
      Выгружено заказов: <span class="text-bold">5 из 5</span>
    </span>
    <span class="unload-card__row">
      Размер выгрузки: <span class="text-bold">{{ item.size }}</span>
    </span>
  </button>
</template>

<script setup>
import DOMPurify from 'dompurify';

defineProps({
  item: {
    type: Object,
    required: true
  }
});

</script>
