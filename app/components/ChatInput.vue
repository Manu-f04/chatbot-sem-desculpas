
<script setup>
import { ref, computed } from 'vue'

const mensagem = ref('')

const emit = defineEmits(['enviar'])

const podeEnviar = computed(() => {
  return mensagem.value.trim().length > 0
})

function enviarMensagem() {
  const texto = mensagem.value.trim()

  if (!texto) {
    return
  }

  emit('enviar', texto)

  mensagem.value = ''
}
</script>

<template>
  <form
    class="chat-input"
    @submit.prevent="enviarMensagem"
  >
    <input
      v-model="mensagem"
      type="text"
      class="chat-input__campo"
      placeholder="Digite sua mensagem..."
      aria-label="Digite sua mensagem"
    />

    <button
      type="submit"
      class="chat-input__botao"
      :disabled="!podeEnviar"
    >
      Enviar
    </button>
  </form>
</template>

<style scoped>
.chat-input {
  display: flex;
  gap: 10px;
  padding: 15px;
  background-color: #1b1b1b;
  border-top: 1px solid #333;
}

.chat-input__campo {
  flex: 1;
  min-width: 0;
  padding: 12px;
  border: 1px solid #444;
  border-radius: 8px;
  background-color: #292929;
  color: white;
  font-size: 14px;
  outline: none;
}

.chat-input__campo:focus {
  border-color: #ff3434;
}

.chat-input__botao {
  padding: 12px 20px;
  border: none;
  border-radius: 8px;
  background-color: #ff3434;
  color: white;
  font-weight: bold;
  cursor: pointer;
}

.chat-input__botao:hover:not(:disabled) {
  background-color: #e52d2d;
}

.chat-input__botao:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

@media (max-width: 480px) {
  .chat-input {
    padding: 10px;
  }

  .chat-input__botao {
    padding: 10px 14px;
  }
}
</style>
