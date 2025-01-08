<template>
  <BlogPosts v-slot="{ posts }" :limit="limit">
    <div v-for="post in posts" :key="post._path">
      <NuxtLink :to="post._path">{{ post.title }}</NuxtLink>
    </div>
  </BlogPosts>
</template>
<script setup>
defineProps({
  limit: {
    type: Number,
    default: null,
  },
});
</script>
