<template>
  <h1>Ninja reaction timer</h1>
  <button :disabled='isPlaying' @click="start">Play</button>
  <!-- we can react to a custom event by listening  for it just like we would listen to any normal event -->
  <Block :delay="delay" v-if="isPlaying" @end='endGame'/>

  <p v-if="showResult">Reaction time is: {{score}}ms</p>
  <Results v-if="showResult" :score="score"/>
  

</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: "App",
  components: {
    Block,Results
  },
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
      showResult: false
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.showResult = false;
    },
    // When reacting to a custom event created by emitting from the child component we can get the data passed in as the second argument of the $emit() function as the first argument to whatever function we're using to respond to that event
    endGame(reactionTime){
      this.score = reactionTime;
      this.isPlaying = false;
      this.showResult = true
    }
  },
};
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
button{
  background-color: #0faf87;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}

button:disabled{
  opacity: 0.2;
  cursor: not-allowed;
}


</style>
