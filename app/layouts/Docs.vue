<script lang="ts" setup>
const { data: link } = await useAsyncData("content", () =>
  queryCollection("content").all()
);
</script>

<template>
  <div class="w-full max-w-(--ui-container) mx-auto px-4 sm:px-6 lg:px-8">
    <div class="flex flex-col lg:grid lg:grid-cols-10 lg:gap-10">
      <!-- ASIDE -->
      <aside
        class="hidden overflow-y-auto lg:block lg:max-h-[calc(100vh-var(--ui-header-height))] lg:sticky lg:top-(--ui-header-height) py-8 lg:ps-4 lg:-ms-4 lg:pe-6.5 lg:col-span-2"
      >
        <div class="relative">
          <div></div>
          <nav>
            <ul class="isolate -mx-2.5 -mt-1.5">
              <li>
                <button>
                  <!--[--><!--[--><!--[--><!--[--><!----><!--]--><span
                    class="truncate"
                    ><!--[-->Getting Started<!--]--><!----></span
                  ><span class="ms-auto gap-1.5 items-center hidden"
                    ><!--[--><!----><span
                      class="iconify i-lucide:chevron-down size-5 transform transition-transform duration-200 shrink-0 group-data-[state=open]:rotate-180"
                      aria-hidden="true"
                      style=""
                    ></span
                    ><!--]--></span
                  ><!--]--><!--]--><!--]-->
                </button>
                <div
                  class="data-[state=open]:animate-[accordion-down_200ms_ease-out] data-[state=closed]:animate-[accordion-up_200ms_ease-out] overflow-hidden focus:outline-none"
                >
                  <ul class="ms-5 border-s border-default">
                    <li
                      v-for="item in link"
                      :id="item.id"
                      class="ps-1.5 -ms-px"
                    >
                      <!--[--><a
                        :href="item.path"
                        class="group relative w-full px-2.5 py-1.5 before:inset-y-px before:inset-x-0 flex items-center gap-1.5 text-sm before:absolute before:z-[-1] before:rounded-md focus:outline-none focus-visible:outline-none focus-visible:before:ring-inset focus-visible:before:ring-2 focus-visible:before:ring-primary text-muted after:absolute after:-left-1.5 after:inset-y-0.5 after:block after:w-px after:rounded-full after:transition-colors hover:text-highlighted data-[state=open]:text-highlighted transition-colors"
                        ><!--[--><!--[--><!--[--><span
                          class="iconify i-lucide:house shrink-0 size-4 mr-1 text-dimmed group-hover:text-default group-data-[state=open]:text-default transition-colors"
                          aria-hidden="true"
                          style=""
                        ></span
                        ><span class="truncate">{{ item.title }}</span></a
                      >
                    </li>
                  </ul>
                </div>
              </li>
            </ul>
          </nav>
        </div>
      </aside>
      <!-- BODY -->
      <div class="lg:col-span-8">
        <div class="flex flex-col lg:grid lg:grid-cols-10 lg:gap-10">
          <!-- BODY:CONTENT -->
          <div class="lg:col-span-8"></div>

          <!-- BODY:TABLE OF CONTENT -->
          <div>TOC</div>
        </div>
      </div>
    </div>
  </div>
</template>
