<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <h1>Sorry We Missed Brakence</h1>

    <p>That's mf whack I was really looking forward to going with you</p>

    <p>So I made a website that has my top 5 Brakence songs to you</p>

    <p style="font-weight: bold">Make sure you have SOUND ON, it's important, and make sure you go all the way to the end</p>

    
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