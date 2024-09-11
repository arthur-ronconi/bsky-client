<template>
  <nav class="w-96 px-4 gap-8 flex flex-col h-full pt-16">
    <button class="rounded-full bg-gray-500 w-12 h-12 overflow-hidden">
      <img class="w-12 h-12 " :src="avatar" />
    </button>
    <ul class="flex flex-col gap-2">
      <NuxtLink to="/" class="nav-btn">
        <Icon name="uil:home-alt"></Icon>
        <span class="font-bold text-lg">
          Home
        </span>
      </NuxtLink>
      <button class="nav-btn">
        <Icon name="uil:sign-out-alt"></Icon>
        <span class="font-bold text-lg">
          Sair
        </span>
      </button>
    </ul>
  </nav>
</template>

<script setup lang="ts">
const actor_data = useState('actor_data');
const avatar = actor_data.value.avatar;
</script>

<style scoped lang="scss">
.nav-btn {
  @apply flex items-center gap-2 hover:bg-gray-800 p-2 rounded;
}
</style>