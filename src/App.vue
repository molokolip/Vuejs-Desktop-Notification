<script setup>
import HelloWorld from './components/HelloWorld.vue'

console.log(Notification.permission);

if (Notification.permission === "granted") {
  alert("Permission granted");

}
else if (Notification.permission !== "denied") {
  Notification.requestPermission().then(permission => {
    console.log(permission);
  })
}

function showNotification() {
  const notification = new Notification("Mphalane", {
    body:"You are Hired"
  });

  notification.onclick = (e) => {
    window,location.href = "https://mphalane.co.ls/";
  };
}


</script>

<template>
<HelloWorld/>
  <div id="app">
    <button v-on:click="showNotification()">Send Notification</button>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: function() {
    return {
      connection: null
    }
  },
  methods: {

    sendMessage: function(message) {
      console.log("Hello")
      console.log(this.connection);
      this.connection.send(message);
    }
  },
  created: function() {
    console.log("Starting connection to WebSocket Server")
    this.connection = new WebSocket(" wss://demos.mphalane.co.ls/ws/chat/")

    this.connection.onmessage = function(event) {
      console.log(event);
    }

    this.connection.onopen = function(event) {
      console.log(event)
      console.log("Successfully connected to mphalane  websocket")
    }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
