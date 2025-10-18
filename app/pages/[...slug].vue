<script setup lang="ts">
const route = useRoute();

const path = computed(() => {
  const slug = route.params.slug;
  const fullPath = Array.isArray(slug)
    ? slug.join("/")
    : slug
    ? slug
    : "getting-started/index";

  return "/" + fullPath;
});

const { data: page } = await useAsyncData(route.path, () => {
  return queryCollection("content").path(path.value).first();
});

definePageMeta({
  layout: "docs",
});
</script>

<template>
  <template v-if="page">
    <div class="flex flex-col lg:grid lg:grid-cols-10 lg:gap-10">
      <!-- BODY:CONTENT -->
      <div class="lg:col-span-8">
        <article class="prose dark:prose-invert">
          <ContentRenderer :value="page" />
        </article>
      </div>

      <!-- BODY:TABLE OF CONTENT -->
      <aside
        v-if="page.body?.toc?.links?.length"
        class="hidden lg:block lg:col-span-2 sticky top-18 self-start h-[calc(100vh-6rem)] overflow-y-auto p-4 border-l border-gray-200 dark:border-gray-800 text-sm"
      >
        <h3 class="font-semibold text-gray-600 dark:text-gray-300 mb-3">
          On this page
        </h3>

        <nav>
          <ul class="space-y-2">
            <li v-for="link in page.body.toc.links" :key="link.id">
              <NuxtLink
                :to="`#${link.id}`"
                class="block py-1 pl-2 border-l border-transparent hover:border-primary hover:text-primary transition-colors"
              >
                {{ link.text }}
              </NuxtLink>

              <!-- Render sub-links (## → ###) -->
              <ul v-if="link.children?.length" class="ml-4 space-y-1">
                <li v-for="child in link.children" :key="child.id">
                  <NuxtLink
                    :to="`#${child.id}`"
                    class="block py-1 pl-2 border-l border-transparent hover:border-primary hover:text-primary transition-colors text-sm"
                  >
                    {{ child.text }}
                  </NuxtLink>
                </li>
              </ul>
            </li>
          </ul>
        </nav>
      </aside>
    </div>
  </template>
  <template v-else>
    <div class="min-h-screen flex items-center justify-center">
      <h1>Page Not Found</h1>
      <p>Oops! The content you're looking for doesn't exist.</p>
      <NuxtLink to="/">Go back home</NuxtLink>
    </div>
  </template>
</template>
