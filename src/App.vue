<template>
  <div id="app">
    <router-view />
    <ChatButton />
  </div>
</template>

<script>
import ChatButton from './components/ChatButton.vue'

export default {
  name: 'App',
  components: {
    ChatButton
  }
}
</script>

<style>
/* Global Styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  line-height: 1.6;
  color: #333;
}

#app {
  min-height: 100vh;
}
</style>
