<template>
  <div>
    This page is about me.
    <button @click="enableLayout('default')">use default layout</button>
    <button @click="enableLayout('another')">use custom layout</button>
  </div>
</template>
<script setup>
useSeoMeta({
  title: "About me",
  description: "This page tells a little bit about me",
  ogTitle: "About me",
  ogDescription: "This page tells a little bit about me",
  ogImage: "[og:image]",
  ogUrl: "[og:url]",
  twitterTitle: "About me",
  twitterDescription: "This page tell a little bit about me",
  twitterImage: "[twitter:image]",
  twitterCard: "summary",
});

useHead({
  htmlAttrs: {
    lang: "en",
  },
  link: [
    {
      rel: "icon",
      type: "image/png",
      href: "/favicon.png",
    },
  ],
});
// definePageMeta({
//   layout: "another",
// });
function enableLayout(layout) {
  setPageLayout(layout);
}
</script>
