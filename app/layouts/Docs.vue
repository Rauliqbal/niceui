<script lang="ts" setup>
const { data: link } = await useAsyncData("content", () =>
  queryCollection("content").all()
);

const route = useRoute();

// const { data: navigation } = await useAsyncData('docs-navigation', () => useContentNavigation())
const { data: navigation } = await useAsyncData("navigation", () => {
  return queryCollectionNavigation("content");
});
</script>

<template>
  <div>
    <!-- Header -->
    <AppNavbar />

    <main class="min-h-screen">
      <div class="w-full max-w-[90rem] mx-auto sm:px-6 lg:px-8">
        <div class="flex flex-col lg:grid lg:grid-cols-10 lg:gap-10">
          <!-- ASIDE -->
          <aside class="lg:col-span-2 w-72 p-6 overflow-y-auto hidden md:block">
            <nav class="space-y-8">
              <div v-for="section in navigation" :key="section.path">
                <h2
                  class="text-sm font-semibold text-neutral-500 uppercase tracking-wide mb-3 flex items-center gap-2"
                >
                  <Icon
                    v-if="section.icon"
                    :name="section.icon"
                    class="w-4 h-4"
                  />
                  {{ section.title }}
                </h2>
                <ul
                  class="border-l border-neutral-200 dark:border-neutral-800 pl-3 space-y-1"
                >
                  <li v-for="link in section.children" :key="link.path">
                    <NuxtLink
                      :to="link.path"
                      class="block py-1.5 px-2 rounded-lg text-sm text-neutral-700 dark:text-neutral-300 hover:text-emerald-500 hover:bg-neutral-100 dark:hover:bg-neutral-800"
                      :class="{
                        'text-emerald-500 font-medium bg-neutral-50 dark:bg-neutral-800':
                          route.path === link.path,
                      }"
                    >
                      {{ link.title }}
                    </NuxtLink>
                  </li>
                </ul>
              </div>
            </nav>
          </aside>

          <!-- BODY -->
          <div class="lg:col-span-8">
            <div class="flex flex-col lg:grid lg:grid-cols-10 lg:gap-10">
              <!-- BODY:CONTENT -->
              <div class="lg:col-span-8">
                <slot />
              </div>

              <!-- BODY:TABLE OF CONTENT -->
              <div>TOC</div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
