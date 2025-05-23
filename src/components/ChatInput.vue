<script setup lang="ts">
import { ref } from 'vue';

const message = ref('');
const emit = defineEmits(['send']);

const sendMessage = () => {
  if (!message.value.trim()) return;
  emit('send', message.value);
  message.value = '';
};
</script>

<template>
  <div class="p-4 bg-white flex border-t border-slate-200">
    <input
      v-model="message"
      @keyup.enter="sendMessage"
      placeholder="Send a message"
      type="text"
      class="flex-1 p-2 rounded-lg bg-slate-100 text-slate-800 focus:outline-none focus:ring-2 focus:ring-green-400"
    />
    <button
      @click="sendMessage"
      class="ml-2 px-4 py-2 bg-green-500 hover:bg-green-600 text-white rounded-lg transition duration-200"
    >
      Send
    </button>
  </div>
</template>

