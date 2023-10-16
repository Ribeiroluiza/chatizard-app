<template>
  <v-app>
    <v-main>
      <v-app-bar color="#FF0070">
        <v-icon>mdi-view-sequential</v-icon>
        <div class="d-flex align-center justify-center" style="flex-grow: 1;">
          <v-toolbar-title>Comentários</v-toolbar-title>
        </div>
        <v-btn @click="deletarAllMessages()" icon color="#FF0070">
          <v-icon>mdi-delete</v-icon>
        </v-btn>
        <v-btn icon @click="toggleMenu" color="white">
          <v-icon style="color:white">mdi-menu</v-icon>
        </v-btn>
        Chatizard
      </v-app-bar>
      <v-card v-for="(message, index) in messages" :key="index" :class="message.nome !== 'Eu' ? 'teal' : 'purple'" outlined class="ma-2">
        <message-card :messageProp="message" :editar="editmessage" @delete="deletarMessage"/>
      </v-card>
      <!-- rodapé -->
      <BottomBar @send-message="addMessage($event)"/>
    </v-main>
  </v-app>
</template>

<script>
import MessageCard from './components/MessageCard.vue'
import BottomBar from './components/BottomBar.vue'
export default {
  components: {
    MessageCard,
    BottomBar
  },
  data() {
    return {
      messages: [
        {
          id: 1,
          nome: 'Yuuto Kunihiro',
          text: 'Meu pokemon favorito é o Swampert pois além do mudkipser o pokemon mais fofo do mundo, ele evolui pro monstro mais destruidor de Hoenn!!!'
        },
      ],
    }
  },
  methods: {
    addMessage(e) {
      const message = {
        id: Math.random(),
        nome: e.nome,
        text: e.text
      }
     this.messages.push(message)
    },
    deletarAllMessages(){
      this.messages = []
    },
    deletarMessage(id){
      this.messages=this.messages.filter(message=> message.id !== id)
    },
    editmessage(id, novoTexto){
      const message = this.messages.find((message) => message.id === id);
      message.text = novoTexto
    }
  }
  }
</script>