<template>
  <div class="chat-container">
    <div class="messages" ref="messagesEnd">
      <div
        v-for="(msg, idx) in messages"
        :key="idx"
        :class="['message', msg.role === 'user' ? 'user' : 'bot']"
      >
        {{ msg.content }}
      </div>
    </div>
    <form class="input-area" @submit.prevent="sendMessage">
      <input
        v-model="input"
        type="text"
        placeholder="Type your message..."
        autocomplete="off"
        :disabled="loading"
      />
      <button type="submit" :disabled="loading || !input">Send</button>
    </form>
  </div>
</template>

<script setup>
import { ref, nextTick } from 'vue'
const input = ref('')
const messages = ref([])
const loading = ref(false)
const messagesEnd = ref(null)

async function sendMessage() {
  if (!input.value.trim()) return
  messages.value.push({ role: 'user', content: input.value })
  loading.value = true
  const userInput = input.value
  input.value = ''
  await nextTick()
  messagesEnd.value.scrollTop = messagesEnd.value.scrollHeight

  try {
    const res = await fetch('http://localhost:8000/chat', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ message: userInput })
    })
    const data = await res.json()
    messages.value.push({ role: 'bot', content: data.response })
    await nextTick()
    messagesEnd.value.scrollTop = messagesEnd.value.scrollHeight
  } catch (e) {
    messages.value.push({ role: 'bot', content: 'Error: Could not reach backend.' })
  }
  loading.value = false
}
</script>

<style>
.chat-container {
  max-width: 600px;
  margin: 40px auto;
  border: 1px solid #eee;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  height: 80vh;
  background: #fafafa;
  box-shadow: 0 2px 8px #0001;
}
.messages {
  flex: 1;
  overflow-y: auto;
  padding: 16px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}
.message {
  max-width: 80%;
  padding: 10px 16px;
  border-radius: 16px;
  word-break: break-word;
  font-size: 1rem;
  line-height: 1.5;
}
.user {
  align-self: flex-end;
  background: #d1e7dd;
  color: #222;
}
.bot {
  align-self: flex-start;
  background: #e9ecef;
  color: #222;
}
.input-area {
  display: flex;
  border-top: 1px solid #eee;
  padding: 12px;
  background: #fff;
}
.input-area input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 6px;
  font-size: 1rem;
  margin-right: 8px;
}
.input-area button {
  padding: 0 18px;
  border: none;
  background: #0d6efd;
  color: #fff;
  border-radius: 6px;
  font-size: 1rem;
  cursor: pointer;
  transition: background 0.2s;
}
.input-area button:disabled {
  background: #aaa;
  cursor: not-allowed;
}
</style>