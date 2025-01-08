<template>
  <BlogPosts v-slot="{ posts }">
    <div v-for="post in getPosts(posts)" :key="post._path">
      <NuxtLink :to="post._path">{{ post.title }}</NuxtLink>
    </div>
  </BlogPosts>
</template>
<script setup>
const props = defineProps({
  limit: {
    type: Number,
    default: null,
  },
});
function getPosts(posts) {
  const shortPosts = [];

  if (props.limit && posts.length > props.limit) {
    return posts.slice(0, props.limit);
  } else {
    return posts;
  }
}
</script>
