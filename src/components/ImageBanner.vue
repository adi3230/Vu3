<script setup>
const props = defineProps({
  mobileImage: {
    type: String,
  },
  tabletImage: {
    type: String,
  },
  desktopImage: {
    type: String
  }
})
</script>

<template>
  <div class="image-banner-wrapper">
    <picture>
      <source media="(min-width: 1024px)" :srcset="props.desktopImage">
      <source media="(min-width: 768px)" :srcset="props.tabletImage">
      <img class="image-banner-wrapper__image" :src="props.mobileImage" alt="Image banner">
    </picture>
  </div>
</template>

<style scoped>

</style>