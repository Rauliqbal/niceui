<script setup lang="ts">
const { data } = await useAsyncData(() =>
  queryCollection("content").path("/getting-started").first()
);

useSeoMeta({
  title: data.value?.title,
  description: data.value?.description,
});

definePageMeta({
  layout: "docs",
});
</script>

<template>
  <NuxtLayout>
    <ContentRenderer v-if="data" :value="data" />
    <div v-else>Home not found</div>
  </NuxtLayout>
</template>
