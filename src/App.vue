<template>

<div class = "top">
  <h2> Total: {{total}}</h2>
  <h2> Time Remaining: {{timeRemaining}}s </h2>
</div>

<div class = "sky">

<Duck v-if = "isPlaying"  :delay = "delay" @hit="handleHit"/>
<Duck v-if = "isPlaying"  :delay = "1500" @hit="handleHit"/>
<Duck v-if = "isPlaying"  :delay = "1000" @hit="handleHit"/>
<Duck v-if = "isPlaying"  :delay = "3000" @hit="handleHit"/>


<h1 class = "score"> {{score}}</h1>

</div>


<div class = "ground">
  <button class="btn" @click = "startGame">Start</button>

    <button class = "restart" @click = "newGame">New Game</button>


    <button class="btn" @click = "stopGame">Stop</button>


</div>

 <!-- <HelloWorld msg="Welcome to Your Vue.js App"/>-->

</template>

<script>

import Duck from './components/Duck.vue'
//import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    Duck
  
  },

    data() {
    return {
      score: 0,
      total: 0,
      timeRemaining: 0,
      isPlaying: false,
      delay: 2000
    };
  },
  methods: {
    startGame() {

      const interval = setInterval( () => {
        this.timeRemaining -= 1;
        if(this.timeRemaining === 0) {
          this.stopGame();
          clearInterval(interval);
        }
      }, 1000)

      this.timeRemaining = 10;
      this.isPlaying = true;

    
    },
    stopGame() {
      this.isPlaying = false;
    },

    handleHit(responseTime) {

      this.score = (this.delay - responseTime) * 4;

      this.total += this.score;

    },

    newGame() {

      const interval = setInterval( () => {
        this.timeRemaining -= 1;
        if(this.timeRemaining === 0) {
          this.stopGame();
          clearInterval(interval);
        }
      }, 1000)


      this.score = 0;
      this.total = 0;
      this.timeRemaining = 10;
      this.isPlaying = true;
      this.delay = 2000;
    }
  }
}

</script>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

}


.top {
  height: 10vh;
  background-color: rgb(255, 253, 208);
}

.sky {
  background: lightskyblue;
  height: 70vh;
  position: relative;
}

.ground {

  height: 20vh;
  background: green;

}

.btn {
  padding: 1em 5em;
  border: none;
  margin: 1em 1em;
  font-size: 1.5rem;
  background-color: rgb(255, 253, 208);
  
}

.restart {
  padding: 0.3em 1em;
  border: none;
  margin: 0.5em 0.5em;
  font-size: 0.7rem;
  justify-content: center;
  background-color: rgb(255, 253, 208);

}

.score {
  padding: 12px;
}
</style>
