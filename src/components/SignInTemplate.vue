<template>
  <div
    class="min-h-screen bg-gray-900 flex flex-col justify-center text-center"
  >
    <div
      class="w-8/12 mx-auto py-8 px-8 rounded-2xl shadow-gray-900 bg-slate-400 shadow"
    >
      <h2 class="font-bold">Login</h2>
      <form class="mx-auto w-fit max-w-xs m mt-4" @submit.prevent="signIn">
        <input type="email" required placeholder="email" v-model="email" />
        <input
          type="password"
          required
          placeholder="password"
          v-model="password"
        />
        <div v-if="errorMsg" class="text-red-900">{{ errorMsg }}</div>
        <button class="my-5 mx-auto transition ease-in-out delay-50">
          Log in
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import useAuth from '../composables/useAuth.js';

const email = ref('');
const password = ref('');

const { login, isAuthenticated, errorMsg } = useAuth();
const router = useRouter();

//signIn admin > if authenticated > redirect to /upload
const signIn = async () => {
  await login(email.value, password.value);
  if (isAuthenticated.value) {
    router.push('/upload');
  }
};
</script>

<style scoped>
input {
  @apply w-full p-2 pl-3 rounded-xl border-4 border-solid bg-gray-100 border-gray-100 my-3 outline-none;
}

button {
  @apply bg-slate-500
        rounded-3xl
        font-bold
        px-8
        py-3
        border-0
        active:scale-90;
}
.container {
  @apply flex
        flex-col
        justify-center
        w-11/12
        max-w-screen-lg
        my-12
        mx-auto
        py-4
        px-1
        sm:py-8
        sm:px-8
        rounded-2xl
        shadow-gray-900
        bg-slate-400
        shadow;
}
</style>
