<script setup lang="ts">
import { useUserStore } from '../stores/user';
import { useRouter } from 'vue-router';
import robotImage from '../assets/icons8-robot-40.png';

const userStore = useUserStore();
const router = useRouter();

const logout = () => {
  userStore.logout();
  router.push('/');
};
</script>

<template>
  <div class="py-4 px-6 bg-white shadow-md flex justify-between items-center rounded-b-lg border-b border-slate-200">
    <img :src="robotImage" alt="Chat AI" class="w-8 h-8" />
    <h1 class="text-lg font-semibold text-slate-900">Chat AI</h1>
    <button
      @click="logout"
      class="text-slate-600 hover:text-green-500 transition-colors"
    >
      Logout
    </button>
  </div>
</template>

