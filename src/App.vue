<script setup lang="ts">
import { ref, onMounted } from "vue";
import fl_icon from "./assets/fl_icon.png"

onMounted(() => {
  const socket = new WebSocket("wss://16c2-46-22-26-85.ngrok-free.app");

  socket.onopen = function (event) {
    console.log("Verbindung hergestellt.");
  };

  socket.onmessage = function (event) {
    console.log("Nachricht vom Laptop: ", event.data);
  };

  function sendCommand(command) {
    socket.send(command);
  }

  socket.onerror = function (error) {
    console.log("Fehler: ", error);
  };

  socket.onclose = function () {
    console.log("Verbindung geschlossen.");
  };
});
</script>

<template>
  <div>
    <button><fl_icon/></button>
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
