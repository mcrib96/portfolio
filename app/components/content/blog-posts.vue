<template>
  <slot :posts="posts">
    <section class="not-prose font-mono">
      <div class="column text-gray-400 text-sm">
        <div>date</div>
        <div>title</div>
      </div>
      <ul>
        <li v-for="post in posts" :key="post._path">
          <NuxtLink
            :to="post._path"
            class="column hover:bg-gray-100 dark:hover:bg-gray-800"
          >
            <div>
              <span v-if="post.displayYear"> {{ post.year }} </span
              ><span v-else> &nbsp;&nbsp;&nbsp;&nbsp; </span>
            </div>
            <div>
              {{ post.title }}
            </div>
          </NuxtLink>
        </li>
      </ul>
    </section>
  </slot>
</template>

<script setup>
const { data } = await useAsyncData("blog-list", () => {
  const query = queryContent("/blog")
    .where({ _path: { $ne: "/blog" } })
    .only(["_path", "title", "publishedAt"])
    .sort({ publishedAt: -1 });
  return query.find();
});
const posts = computed(() => {
  if (!data.value) {
    return [];
  }
  const result = [];
  let lastYear = null;
  for (let post of data.value) {
    const year = new Date(post.publishedAt).getFullYear();
    const displayYear = year !== lastYear;
    lastYear = year;
    post.displayYear = displayYear;
    post.year = year;
    result.push(post);
  }
  return result;
});
</script>
<style scoped>
.column {
  @apply flex items-center space-x-8 py-2 border-b border-gray-200 dark:border-gray-700;
}
</style>
