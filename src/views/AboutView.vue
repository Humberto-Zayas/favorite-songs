<template>
  <main>
    <h1>Share a playlist or other call to action</h1>

    <p>Share a link to a place they can listen to more songs on the platform you'd like them to use.</p>

    <a target="_blank" href="https://untitled.stream/library/project/LfcveRZJG8DKFyNrbtd-S">Click Here For The Playlist</a>
    <router-link class="darkBtn" to="/">Re-Start</router-link>
  </main>
</template>

<style scoped>

main {
  height: 100vh;
  display: flex;
  padding: 2em;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
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
