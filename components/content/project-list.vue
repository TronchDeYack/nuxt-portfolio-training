<script setup>
const { error, pending, data } = await useFetch('https://api.github.com/users/tronchdeyack/repos')

const repos = computed(() => data.value.filter(repo => repo.description).sort((a, b) => b.stargazers_count - a.stargazers_count ))
</script>

<template>
  <div class="not-prose">
    <section v-if="pending">Loading...</section>
    <section v-else-if="error">Something went wrong</section>
    <section v-else>
      <ul class="grid grid-cols-1 gap-4">
        <li 
          v-for="repository in repos"
          class="border border-gray-200 dark:border-gray-800 rounded-sm p-4 hover:bg-gray-200 dark:hover:bg-gray-800 font-mono"
          :key="repository.id"
        >
          <a :href="repository.html_url" target="_blank">
            <div class="flex items-center justify-between text-sm">
              <div class="font-semibold">
                {{ repository.name }}
              </div>
              <div>{{ repository.stargazers_count }} ⋆</div>
            </div>
            <p class="text-sm">
              {{ repository.description }}
            </p>
          </a>
        </li>
      </ul>
    </section>
  </div>
</template>