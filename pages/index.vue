<template>
  <div>
    app index
  </div>
</template>

<script setup lang="ts">
const actor_data = useState('actor_data');
const actor = actor_data.value.handle;

const { data } = await agent.app.bsky.actor.getProfile({
  actor
});
console.log(data);
</script>

<style lang="scss" scoped>
.hello {
  color: red;
}
</style>