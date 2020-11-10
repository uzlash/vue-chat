<template>
  <div id="app">
    <div class="header">
      <h1>Chatroom</h1>
      <p class="username">Username: {{ username }}</p>
      <p class="online"> Users Online: {{ users.length }}</p>
    </div>
  </div>
</template>

<script>
import io from 'socket.io-client'

export default {
  name: 'App',
  components: {},
  data: function() {
    return {
      username: "",
      socket: io('http://localhost:3366'),
      messages: [],
      users: []
    }
  },
  methods: {
    joinServer() {
      this.socket.on('loggedIn', data => {
        this.messages = data.messages
        this.users = data.users
        this.socket.emit('newUser', this.username)
      })
    }
  },
  mounted() {
    this.username = 'Uzlash'
    this.joinServer()
  }
}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
#app {
  display: flex;
  flex-direction: column;
  height: 100vh;
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
}
</style>
