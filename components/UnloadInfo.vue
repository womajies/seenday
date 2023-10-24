<template>
  <template v-if="!pending">
    <div class="unload-info__header">
      <div class="unload-info__header-id">{{ itemInfo.id }}</div>
      <div class="unload-info__header-name">{{ itemInfo.event }} {{ itemInfo.event }}</div>
    </div>
    <div class="unload-info__zip block">
      <div class="unload-info__zip-advice">
        <i class="fa-solid fa-lightbulb" style="color: #2a6ee5;"/> Если после клика на ссылку загрузка не пошла, проверьте не блокирует ли браузер скачивание архива.
      </div>
      <h3 class="unload-info__zip-title text-bold">Ссылка для скачивания архива Выгрузки (.zip):</h3>
      <a :href="itemInfo.download_link" class="link" download>{{ itemInfo.download_link }}</a>
      <button class="unload-info__zip-copy span-link" type="button" @click="copyLink">Скопировать ссылку</button>
      <button class="unload-info__close button" data-color="red" @click="$emit('close-info')"><span class="unload-info__close-icon">X</span><span class="unload-info__close-text">Закрыть</span></button>
    </div>
  </template>
  <div v-else-if="error" class="block">
    {{ error?.message }}
  </div>
  <div v-else class="block">
    Загрузка...
  </div>
</template>

<script setup>
const props = defineProps({
  item: {
    type: Object,
    required: true
  }
});

defineEmits(['close-info']);

const downloadLink = ref(null);
const itemData = ref(null);

const { data, pending, error } = await useAPIFetch(`e.scripts?page=pages:unload&event=get&unload_id=${props.item.id}`);
itemData.value = data;

const itemInfo = computed(() => {
  const info = JSON.parse(itemData.value.value).response.data[0];
  downloadLink.value = info.download_link;
  return info;
});


watch(() => props.item, async (newItem) => {
  const { data } = await useAPIFetch(`e.scripts?page=pages:unload&event=get&unload_id=${newItem.id}`);
  itemData.value = data;
});

const copyLink = () => {
  navigator.clipboard.writeText(downloadLink.value);
};

</script>
