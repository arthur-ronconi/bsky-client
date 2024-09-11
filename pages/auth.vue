<template>
  <div class="flex items-center justify-center h-full">
    <div class="bg-gray-800 rounded p-4 flex flex-col gap-4 w-80">
      <h1 class="font-bold">
        bsky-client
      </h1>
      <Input label="Email" name="email" v-model="user_data.email" />
      <Input label="Senha" name="password" type="password" v-model="user_data.password"
        :password_visible="user_data.password_visible"
        @toggle-visibility="user_data.password_visible = !user_data.password_visible" />
      <button
        class="h-10 rounded bg-gray-300 text-gray-950 hover:brightness-125 active:brightness-75 flex items-center justify-center"
        @click="signIn">
        <Icon v-if="is_loading" name="uil:spinner" class="animate-spin text-gray-950" />
        <span v-else>
          Continuar
        </span>
      </button>
    </div>
  </div>
</template>

<script setup lang="ts">
definePageMeta({
  layout: 'auth'
});

const router = useRouter();

const actor_data = useState('actor_data');

const user_data = reactive({
  email: '',
  password: '',
  password_visible: false
});
const is_loading = ref(false);

type LoginData = {
  identifier: string,
  password: string;
};

const signIn = async () => {
  try {
    is_loading.value = true;
    const login_data: LoginData = {
      identifier: user_data.email,
      password: user_data.password
    };

    const login_response = await agent.login(login_data);

    const get_profile_response = await agent.app.bsky.actor.getProfile({
      actor: login_response.data.handle
    });

    actor_data.value = get_profile_response.data;

    router.push('/');
  } catch (err) {
    alert(err.data);
  } finally {
    is_loading.value = false;
  }
};
</script>

<style scoped></style>