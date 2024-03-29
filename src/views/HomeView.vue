<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <h1>Virtual Mixtape Idea</h1>

    <p>Highlight special songs from a mixtape with creative visuals</p>

    <p>Can be modified to the creators vision (ex: collect emails etc..)</p>

    <p style="font-weight: bold">Share a link to a playlist or product at the end</p>

    
    <router-link class="darkBtn" to="/songs">Start</router-link>
  </main>
</template>

<style scoped>

main {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
  padding: 2em;
  text-align: center;
}
.darkBtn {
  padding: 0.5em 1em;
    border-radius: 1em;
    background-color: #021423;
    font-weight: bold;
}
.startBtn {
  padding: 0.5em 2em;
  background-color: rgb(61, 72, 39);
  border-radius: 1em;
  font-weight: bold;
  text-transform: uppercase;
  cursor: pointer;
}

</style>