<template>
  <main class="unload">
    <Block class="unload-header">
      <template #title>Выгрузка</template>
      <div class="text-bold">Выполняет работу:</div>
      <ul class="unload-header__list">
        <li class="unload-header__item">Собирает фотографии из заказов пользователей.</li>
        <li class="unload-header__item">Выгружает по папкам.</li>
      </ul>
    </Block>
    <div class="unload-info">
      <UnloadInfo v-if="showInfoItem" :item="showInfoItem" @close-info="handleCloseInfo" />
      <UiNotice v-else class="unload-info__notice">
        Для того, чтобы просмотреть информацию о <b class="text-bold">выгрузке</b>, а также ее скачать, нажмите на
        требуемую
        выгрузку в столбце слева.
      </UiNotice>
    </div>
    <UnloadList class="unload-content" @show-info="handleShowInfo" />
  </main>
</template>

<script setup>
const showInfoItem = ref(null);

const handleShowInfo = (evt) => {
  showInfoItem.value = evt;
};

const handleCloseInfo = () => {
  showInfoItem.value = null;
};
</script>
