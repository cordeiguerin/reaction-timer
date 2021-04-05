<template>
  <header>
    <img src="./assets/ninja-left.png" />
    <div id="center-panel">
      <h1>Ninja Reaction Timer</h1><br />
      <h3>Do you have the reactions of a ninja?</h3>
    </div>
    <img src="./assets/ninja-right.png" />
  </header>

  <h2>Game Instructions:</h2>
  <p>When you are ready click the "Start Playing" button below.  After a random period of time another button will appear on-screen.  Click this button as soon as you see it to test your reflexes.</p>

  <!-- When button is clicked, the startPlaying method is activated.  This changes the isPlaying boolean from false to true, which in turn disables the button, preventing the player from clicking this button while waiting for the block section to appear -->
  <button @click="startPlaying" :disabled="isPlaying">Start Playing</button>

  <!-- Block component from Block.vue.  Only shows if isPlaying is true.  Passes the random delay time to Block.vue as a prop -->
  <Block  v-if="isPlaying" :delay="delay" @end="endGame" />
  <Results v-if="showScore" :score="score" />

  <footer>
    <p>Images by <a href="https://pixabay.com/users/davidrockdesign-2595351/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=3620645">DavidRockDesign</a> from <a href="https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=3620645">Pixabay</a></p>
  </footer>
</template>

<script>
import Block from "./components/Block.vue"
import Results from "./components/Results.vue"

export default {
  name: 'App',
  components: { Block, Results },
  data() {
    // Initial data values, before game is started
    return {
      isPlaying: false,
      delay: null,
      score: 0,
      showScore: false
    }
  },
  methods: {
    startPlaying() {
      // produces a random number between 2000ms and 7000ms (2-7 secs).  Note, the random method produces a number between 0 and 1.
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true 
      this.showScore = false
    },
    endGame(reactionTime) {
      this.score = reactionTime
      this.showScore = true
      this.isPlaying = false
    }
  }
}
</script>

<style>
/* global styling */
#app {
  position: relative;
  height: 95vh;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin: 0 auto;
  padding: 0;
  width: 100%;
  border: 2px solid black;
}

/* header styling */
header {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-height: 15vh;
}

header img {
  max-height: 15vh;
  flex-grow: 1;
}

div#center-panel {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  flex-grow: 20;
  background-image: url("./assets/centre-piece.png");
  background-size: 100% 15vh;
  max-height: 15vh;
}

/* text styling */
h1 {
  font-size: 2rem;
  color: antiquewhite;
  margin: 0 auto;
}

h3 {
  color: antiquewhite;
  margin: 0 auto;
}

p {
  padding: 1% 5%;
}

/* button styling */
button {
  background-color: #A54F1A;
  color: antiquewhite;
  width: 20vw;
  padding: 1em;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
}

button:disabled {
  background-color: #C1A832;
  cursor: not-allowed;
}

/* footer styling */
footer {
  position: absolute;
  width: 100vw;
  bottom: 0;
}

/* media query to style title on mobile */
@media only screen and (max-width: 610px){
  h1 {
    font-size: 1rem;
  }
}
</style>
