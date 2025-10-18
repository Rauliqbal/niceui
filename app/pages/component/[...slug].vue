<template>
  <NuxtLayout name="docs">
    <ContentDoc path="/components" :path="'/components/' + route.params.slug" />
  </NuxtLayout>
</template>

<script setup lang="ts">
const route = useRoute();
</script>
