<template>
  <v-container>
    <v-card>
      <v-card-title>Chatbot</v-card-title>
      <v-card-text>
        <div v-for="(msg, idx) in messages" :key="idx">
          <b>{{ msg.role }}:</b> {{ msg.content }}
        </div>
        <v-text-field v-model="input" label="Type your message..." @keyup.enter="sendMessage"/>
        <v-btn @click="sendMessage">Send</v-btn>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      input: "",
      messages: []
    }
  },
  methods: {
    async sendMessage() {
      if (!this.input) return;
      this.messages.push({ role: "User", content: this.input });
      const res = await fetch("http://localhost:8000/chat", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ message: this.input })
      });
      const data = await res.json();
      this.messages.push({ role: "Bot", content: data.response });
      this.input = "";
    }
  }
}
</script> 