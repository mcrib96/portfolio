<template>
  <article class="prose dark:prose-invert max-w-none">
    <ContentDoc v-slot="{ doc }">
      <div class="grid grid-cols-6 gap-16">
        <div :class="{ 'col-span-4': doc.toc, 'col-span-6': !doc.toc }">
          <ContentRenderer :value="doc" />
        </div>
        <div class="col-span-2 not-prose" v-if="doc.toc">
          <aside class="sticky top-8">
            <div class="font-semibold mb-2">Table of Contents</div>
            <nav>
              <TocLinks :links="doc.body.toc.links" :active-id="activeId" />
            </nav>
          </aside>
        </div>
      </div>
    </ContentDoc>
  </article>
</template>

<script setup>
const activeId = ref(null);
onMounted(() => {
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
  const elements = document.querySelectorAll("h2, h3");
  for (const element of elements) {
    observer.observe(element);
  }
  onBeforeUnmount(() => {
    for (const element of elements) {
      observer.unobserve(element);
    }
  });
});
</script>
