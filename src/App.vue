<template>
  <div id="app">
    <div id="start-button" v-if="step === 0">
      <button @click="generateRandomNumber">START</button>
    </div>
    <div v-if="step === 1">
      <div id="star-section" v-for="star in stars">
        <font-awesome-icon icon="star" />
      </div>
      <div id="answer-section">
        <button @click="reset">Reset</button>
        <button class="answer-section"><strong>ANS: {{ answer }}</strong></button>
        <button @click="submitAnswer">Submit</button>
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
export default {
  name: 'app',
  data () {
    return {
      stars: 0,
      answer: '',
      step: 0,
      answers: []
    }
  },
  methods: {
    generateRandomNumber() {
      // Math.floor(Math.random() * (max -min +1)) + min;
      this.stars = Math.floor(Math.random() * (10 - 1 +1) + 1 );
      this.step = 1;
    },

    generateAnswer(num) {
      this.answer = this.answer + num;
    },

    reset() {
      this.answer = '';
    },

    submitAnswer() {
      this.answers.push(this.answer);
      this.reset();
      this.generateRandomNumber(); 
    }
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

#start-button {
  position: absolute;
  top: 35%;
  left: 47%;
}

#start-button button {
  padding: 15px;
  font-size: 2rem;
  font-weight: bold;
  border-radius: 5px;
}

.answer-section {
  background-color: lightblue;
  padding: 15px;
  margin: 0 10px;
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
