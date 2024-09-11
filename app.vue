<template>
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>
<script setup lang="ts">
const actor_data = useState('actor_data', () => { });
</script>
<style>
* {
  font-family: 'Roboto Mono', monospace
}

body {
  @apply bg-gray-950 text-gray-300;
}
</style>
