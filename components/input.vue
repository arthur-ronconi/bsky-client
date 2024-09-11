<template>
  <div class="flex flex-col gap-1">
    <label :for="name" class="text-xs">
      {{ label }}
    </label>
    <div class="relative flex items-center w-full">
      <input :type="inputType" :name="name" class="h-10 rounded bg-gray-900 px-2 text-sm w-full" @input="handleInput">
      <template v-if="type == 'password'">
        <button @click="emit('toggle-visibility')"
          class="absolute right-2 h-full flex items-center hover:brightness-125">
          <Icon name="uil:eye" v-if="password_visible"></Icon>
          <Icon name="uil:eye-slash" v-else></Icon>
        </button>
      </template>
    </div>
  </div>
</template>

<script setup lang="ts">
const emit = defineEmits(['toggle-visibility']);
const model = defineModel();
const props = defineProps({
  type: {
    type: String,
    default: 'text',
    validator: (val) => {
      return ['text', 'number', 'password'].includes(val);
    }
  },
  name: {
    type: String
  },
  label: {
    type: String
  },
  password_visible: {
    type: Boolean
  }
});
const handleInput = (e) => {
  model.value = e.target.value;
};

const inputType = computed(() => {
  if (props.type == 'password' && !props.password_visible) {
    return 'password';
  }
  return 'text';
});
</script>

<style scoped></style>