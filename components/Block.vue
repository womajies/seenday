<template>
  <div class="block">
    <h2 v-if="$slots['title']" class="block__title text-bold">
      <slot name="title"/>
    </h2>
    <slot name="default"/>
  </div>
</template>

<style lang="scss">
.block {
  padding: $inner-gap;

  &__title {
    display: block;
    font-size: 18px*$tem;

    @include start-at(xslg) {
      font-size: 20px*$tem;
    }
  }
}
</style>
