<template>
  <div class="container mx-auto max-w-2xl">
    <header class="flex justify-between items-center mt-5">
      <div>
        <NuxtLink to="/" class="text-xl font-semibold p-2 hover:bg-gray-200"
          >Dan Obregon</NuxtLink
        >
      </div>
      <Menu />
    </header>
    <main class="p-2 mt-10">
      <slot />
    </main>
  </div>
</template>
<script setup>
useHead({
  titleTemplate: "%s - Dan Obregon",
  link: [
    {
      rel: "preconnect",
      href: "https://fonts.googleapis.com",
    },
    {
      rel: "stylesheet",
      link: "https://fonts.googleapis.com/css2?family=Noto+Sans&display=swap",
    },
  ],
});
</script>
<style>
body {
  font-family: "Noto Sans", serif;
  font-optical-sizing: auto;
  font-style: normal;
  font-variation-settings: "wdth" 100;
}
</style>
