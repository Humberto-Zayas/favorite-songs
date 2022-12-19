<template>
  <main>
    <h1>Also here's a playlist from me to you or whateva</h1>

    <p>Wouldn't this make a cool site tho you come and pick 5 songs and then give someone you like a playlist?</p>

    <a target="_blank" href="https://open.spotify.com/playlist/2018d9C9m8IWiUBDMBFq5Z?si=cc55f9d47fa9421e">Click here for the playlist or whatever</a>
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
