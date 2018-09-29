<template>
  <div id="app">
    <div id="start-end">
      <button class="first" v-if="step === 0" @click="startGame">START GAME</button>
      <div v-if="step === 3">
        <p>Game Ended</p>
        <p>Score:</p>
        <button @click="startGame">PLAY AGAIN</button>
      </div>
    </div>
    <div v-if="step === 1">
      <stop-watch />
      <h1>Challenge: {{ challenge }}</h1>
      <div id="star-section" v-for="star in stars">
        <font-awesome-icon icon="star" class="star-icon" />
      </div>
      <div id="answer-section">
        <button @click="reset">RESET</button>
        <button class="answer-section"><strong>ANS: {{ answer }}</strong></button>
        <button @click="submitAnswer">SUBMIT</button>
      </div>
      <div id="select-section">
        <ul class="select-inner-section" v-for="num in 9">
          <li class="select-digit" @click="generateAnswer(num)">{{num}}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import StopWatch from './components/StopWatch';

export default {
  name: 'app',
  data () {
    return {
      stars: 0,
      answer: '',
      step: 0,
      answers: [],
      challenge: 0
    }
  },
  methods: {
    startGame() {
      this.generateRandomNumber();
      this.step = 1;
      this.challenge = 1;
    },

    generateRandomNumber() {
      // Math.floor(Math.random() * (max -min +1)) + min;
      this.stars = Math.floor(Math.random() * (9 - 1 +1) + 1 );
    },

    generateAnswer(num) {
      this.answer = this.answer + num;
    },

    reset() {
      this.answer = '';
    },
 
    submitAnswer() {
      if(this.challenge !== 10) {
        if(this.stars === Number(this.answer)) {
          this.answers.push(this.answer);
          this.challenge++;
          this.reset();
          this.generateRandomNumber(); 
        } else {
          alert('Wrong Answer, please submit another answer')
        }
      } else {
        this.step = 3;
        this.answer = '';
        this.stars = 0;
      }
    }
  },
  components: {
    'stop-watch': StopWatch
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 200px 30%;
  background-color: #E6E6FA;
  padding: 25px;
  border-radius: 3px;
  min-height: 500px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

#star-section {
  display: inline-block;
  padding: 40px 0;
}

.star-icon {
  font-size: 90px
}

#start-end {
  text-align: center;
}

#start-end button {
  padding: 15px;
  font-size: 2rem;
  font-weight: bold;
  border-radius: 5px;
}

#start-end .first {
  margin-top: 30%;
}

#start-end p {
  font-size: 2rem;
  font-weight: bold;
}

#answer-section button  {
  padding: 15px;
  margin: 0 10px;
  font-size: 2rem;
}

.answer-section {
  background-color: lightblue;
}

#select-section {
  padding-top: 40px;
}

.select-inner-section{
  display: inline;
}

.select-digit{
  background-color: lightblue;
  padding: 10px;
  border-radius: 50%;
}
</style>
