
<script setup>
import { ref } from 'vue'

import ChatHeader from '~/components/ChatHeader.vue'
import ChatInput from '~/components/ChatInput.vue'
import MessageContainer from '~/components/MessageContainer.vue'
import MessageBubble from '~/components/MessageBubble.vue'
import TypingIndicator from '~/components/TypingIndicator.vue'

const mensagens = ref([])
const carregando = ref(false)

const mensagemInicial = {
  text: 'Olá! Sou o SEM DESCULPAS. Como posso ajudar você hoje?',
  sender: 'bot',
  time: ''
}

let proximoId = 0
let temporizador = null

function receberMensagem(texto) {
  if (!texto.trim() || carregando.value) {
    return
  }

  mensagens.value.push({
    id: ++proximoId,
    text: texto,
    sender: 'user',
    time: obterHorario()
  })

  carregando.value = true

  // Resposta simulada, sem necessidade de API
  temporizador = setTimeout(() => {
    mensagens.value.push({
      id: ++proximoId,
      text: 'Recebi sua mensagem! Esta é uma resposta de demonstração do chatbot.',
      sender: 'bot',
      time: obterHorario()
    })

    carregando.value = false
    temporizador = null
  }, 1500)
}

function obterHorario() {
  return new Date().toLocaleTimeString('pt-BR', {
    hour: '2-digit',
    minute: '2-digit'
  })
}

onUnmounted(() => {
  if (temporizador) {
    clearTimeout(temporizador)
  }
})
</script>

<template>
  <main class="pagina-chat">
    <section class="chat">
      <!-- Cabeçalho do colega -->
      <ChatHeader />

      <!-- Área de conversa -->
      <div class="area-conversa">
        <!-- Balão inicial -->
        <MessageBubble
          :text="mensagemInicial.text"
          :sender="mensagemInicial.sender"
          :time="mensagemInicial.time"
        />

        <!-- Mensagens enviadas e recebidas -->
        <MessageContainer
          v-if="mensagens.length > 0"
          :messages="mensagens"
        />

        <!-- Indicador de digitação -->
        <TypingIndicator v-if="carregando" />
      </div>

      <!-- Teu componente -->
      <ChatInput @enviar="receberMensagem" />
    </section>
  </main>
</template>

<style scoped>
.pagina-chat {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  background-color: #121212;
}

.chat {
  width: 100%;
  max-width: 1000px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  background-color: #171717;
  border-left: 1px solid #333;
  border-right: 1px solid #333;
}

.area-conversa {
  flex: 1;
  min-height: 0;
  overflow-y: auto;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

@media (max-width: 600px) {
  .area-conversa {
    padding: 12px;
  }
}
</style>
