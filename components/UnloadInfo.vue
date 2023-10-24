<template>
  <div v-if="!pending" class="unload-info">
    <div class="unload-info__zip block">
      <div>

      </div>
      <h3 class="unload-info__zip-title text-bold">Ссылка для скачивания архива Выгрузки (.zip):</h3>
      <a :href="itemInfo.download_link" class="link" target="_blank">{{ itemInfo.download_link }}</a>
      <button class="unload-info__zip-copy span-link" type="button" @click="copyLink">Скопировать ссылку</button>
    </div>
  </div>
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

const downloadLink = ref(null);
const itemData = ref(null);

const { data, pending, error } = await useAPIFetch(`e.scripts?page=pages:unload&event=get&unload_id=${props.item.id}`);
itemData.value = data;

const itemInfo = computed(() => {
  const info = JSON.parse(itemData.value.value).response.data[0];
  console.log(info);
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
