<template>
  <div class="not-prose">
    <section v-if="pending">Loading...</section>
    <section v-else-if="error">Something went wrong... Try again!</section>
    <section v-else>
      <ul class="grid grid-cols-1 gap-4">
        <li
          v-for="repo in repos"
          :key="repo.id"
          class="border border-gray-200 dark:border-gray-800 rounded-sm p-4 hover:bg-gray-200 font-mono dark:hover:bg-gray-800"
        >
          <a :href="repo.html_url" target="_blank">
            <div class="flex items-center justify-between text-sm">
              <div class="font-semibold">
                {{ repo.name }}
              </div>
              <div>{{ repo.stargazers_count }} *</div>
            </div>
            <p class="text-sm">
              {{ repo.description }}
            </p>
          </a>
        </li>
      </ul>
    </section>
  </div>
</template>

<script setup>
const myRepoLink = "https://api.github.com/users/mcrib96/repos";
const { error, pending, data } = await useFetch(myRepoLink);
const repos = computed(() =>
  data.value.filter((repo) => repo.description).sort((a, b) => a.name - b.name)
);
</script>
