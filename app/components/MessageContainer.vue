<template>
  <div ref="chatContainer" class="chat-container">
    <div v-for="(msg, index) in messages" :key="index" class="message" :class="msg.sender === 'user' ? 'user-msg' : 'bot-msg'">
      {{ msg.text }}
    </div>
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from 'vue';

const props = defineProps({
  messages: Array
});

const chatContainer = ref(null);

watch(
  () => props.messages,
  async () => {
    await nextTick();
    if (chatContainer.value) {
      chatContainer.value.scrollTop = chatContainer.value.scrollHeight;
    }
  },
  { deep: true }
);
</script>

<style scoped>
.chat-container {
  height: 400px;
  overflow-y: auto;
  padding: 15px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.message {
  max-width: 70%;
  padding: 10px 14px;
  border-radius: 8px;
  font-size: 14px;
}

.user-msg {
  background-color: #007bff;
  color: white;
  align-self: flex-end;
}

.bot-msg {
  background-color: #e2e6ea;
  color: #333;
  align-self: flex-start;
}
</style>