<script setup>
defineProps({
  text: {
    type: String,
    required: true
  },
  sender: {
    type: String,
    required: true,
    validator: (value) => ['user', 'bot'].includes(value)
  },
  time: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <div
    class="message-bubble"
    :class="`message-bubble--${sender}`"
  >
    <div class="message-bubble__content">
      <span class="message-bubble__sender">
        {{ sender === 'bot' ? 'SEM DESCULPAS' : 'Você' }}
      </span>

      <p class="message-bubble__text">{{ text }}</p>

      <span v-if="time" class="message-bubble__time">
        {{ time }}
      </span>
    </div>
  </div>
</template>

<style scoped>
.message-bubble {
  display: flex;
  width: 100%;
  margin-bottom: 14px;
  animation: bubbleFadeIn 0.2s ease-out;
}

.message-bubble--user {
  justify-content: flex-end;
}

.message-bubble--bot {
  justify-content: flex-start;
}

.message-bubble__content {
  display: flex;
  flex-direction: column;
  gap: 4px;
  max-width: 75%;
  padding: 12px 16px;
  border-radius: 14px;
  line-height: 1.5;
  overflow-wrap: break-word;
  word-break: break-word;
}

/* Balão do Usuário */
.message-bubble--user .message-bubble__content {
  background-color: #ff3434;
  color: #ffffff;
  border-bottom-right-radius: 4px;
}

/* Balão do Bot (tema escuro alinhado ao ChatHeader) */
.message-bubble--bot .message-bubble__content {
  background-color: #1b1b1b;
  color: #f3f4f6;
  border: 1px solid #333333;
  border-left: 3px solid #ff3434;
  border-bottom-left-radius: 4px;
}

.message-bubble__sender {
  font-size: 0.72rem;
  font-weight: 800;
  letter-spacing: 0.03em;
  text-transform: uppercase;
}

.message-bubble--user .message-bubble__sender {
  color: rgba(255, 255, 255, 0.85);
  text-align: right;
}

.message-bubble--bot .message-bubble__sender {
  color: #ff3434;
}

.message-bubble__text {
  margin: 0;
  font-size: 0.95rem;
  white-space: pre-wrap;
}

.message-bubble__time {
  margin-top: 2px;
  font-size: 0.7rem;
  opacity: 0.7;
  text-align: right;
}

@keyframes bubbleFadeIn {
  from {
    opacity: 0;
    transform: translateY(6px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 480px) {
  .message-bubble__content {
    max-width: 86%;
    padding: 10px 14px;
  }

  .message-bubble__text {
    font-size: 0.875rem;
  }
}
</style>