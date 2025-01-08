<template>
  <article class="prose dark:prose-invert max-w-none">
    <ContentDoc>
      <template #not-found>
        <h1>Document not found (404)</h1>
        <br />
        This blog post was not found
      </template>
      <template v-slot="{ doc }">
        <div class="grid grid-cols-6 gap-16">
          <div
            :class="{
              'col-span-6 md:col-span-4': doc.toc,
              'col-span-6': !doc.toc,
            }"
          >
            <ContentRenderer :value="doc" />
          </div>
          <div class="col-span-2 not-prose hidden md:block" v-if="doc.toc">
            <aside class="sticky top-8">
              <div class="font-semibold mb-2">Table of Contents</div>
              <nav>
                <TocLinks :links="doc.body.toc.links" :active-id="activeId" />
              </nav>
            </aside>
          </div>
        </div>
      </template>
    </ContentDoc>
  </article>
</template>

<script setup>
const activeId = ref(null);
onMounted(() => {
  let elements = [];
  const cb = (entries) => {
    for (const entry of entries) {
      if (entry.isIntersecting) {
        activeId.value = entry.target.id;
      }
    }
  };
  const observer = new IntersectionObserver(cb, {
    threshold: 0.5,
    root: null,
  });
  setTimeout(() => {
    elements = document.querySelectorAll("h2, h3");
    for (const element of elements) {
      observer.observe(element);
    }
  }, 150);
  onBeforeUnmount(() => {
    for (const element of elements) {
      observer.unobserve(element);
    }
  });
});
</script>
