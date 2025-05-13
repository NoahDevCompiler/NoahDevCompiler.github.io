<script setup lang="ts">
import { onMounted } from "vue";


let socket: WebSocket;
const calc = "open_calc"
const shutdown = "shutdown"

onMounted(() => {
  socket = new WebSocket("wss://16c2-46-22-26-85.ngrok-free.app");

  socket.onopen = function (event) {
    console.log("Verbindung hergestellt.", event);
  };

  socket.onmessage = function (event) {
    console.log("Nachricht vom Laptop: ", event.data);
  };


  socket.onerror = function (error) {
    console.log("Fehler: ", error);
  };

  socket.onclose = function () {
    console.log("Verbindung geschlossen.");
  };
});

function sendCommand(command:string) {
   if (socket && socket.readyState === WebSocket.OPEN) {
      socket.send(command);
   }    
  }
</script>

<template>
  <div>
    <button @click="sendCommand(calc)"><img src="./assets/fl_icon.jpg"></button>
    <button @click="sendCommand(shutdown)"><fl_icon /></button>
    <button @click="sendCommand(calc)"><fl_icon /></button>
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
