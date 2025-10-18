<script setup lang="ts">
const route = useRoute();
</script>

<template>
  <NuxtLayout name="docs">
    <ContentDoc :path="'/components/' + route" />
  </NuxtLayout>
</template>
