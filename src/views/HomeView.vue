<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';
import { useUserStore } from '../stores/user';
import { useRouter } from 'vue-router';
import robotImage from '../assets/icons8-robot-40.png';

const userStore = useUserStore();
const router = useRouter();

const name = ref('');
const email = ref('');
const loading = ref(false);
const error = ref('');

const createUser = async () => {
  if (!name.value || !email.value) {
    error.value = 'Name and email are required';
    return;
  }

  loading.value = true;
  error.value = '';

  try {
    const { data } = await axios.post(
      `${import.meta.env.VITE_API_URL}/register-user`,
      {
        name: name.value,
        email: email.value,
      }
    );

    userStore.setUser({
      userId: data.userId,
      name: data.name,
    });

    router.push('/chat');
  } catch (err) {
    error.value = 'Something went wrong. Please try again';
  } finally {
    loading.value = false;
  }
};
</script>

<template>
  <div class="h-screen flex items-center justify-center bg-slate-100 text-slate-900">
    <div class="p-8 bg-white rounded-xl shadow-xl w-full max-w-md">
      <img :src="robotImage" alt="" class="mx-auto w-24 h-24 mb-4" />
      <h1 class="text-2xl font-semibold mb-4 text-center">
        Welcome To Chat AI
      </h1>

      <input
        type="text"
        class="w-full p-2 mb-2 bg-slate-200 text-slate-800 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-400"
        placeholder="Name"
        v-model="name"
      />
      <input
        type="email"
        class="w-full p-2 mb-2 bg-slate-200 text-slate-800 rounded-lg focus:outline-none focus:ring-2 focus:ring-green-400"
        placeholder="Email"
        v-model="email"
      />

      <button
        @click="createUser"
        class="w-full p-2 bg-green-500 hover:bg-green-600 text-white rounded-lg transition duration-200"
        :disabled="loading"
      >
        {{ loading ? 'Logging in...' : 'Start Chat' }}
      </button>

      <p v-if="error" class="text-red-500 text-center mt-2">{{ error }}</p>
    </div>
  </div>
</template>

