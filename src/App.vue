<template>
  <div id="app">
    <button @click="generateRandomNumber">Start</button></br>
    <div id="star-section" v-for="star in stars">
      <font-awesome-icon icon="star" />
    </div>
    <div id="answer-section">
      <strong>ANS:</strong> 
    </div>
    <div id="select-section">
      <ul class="select-inner-section" v-for="num in 9">
        <li class="select-digit">{{num}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      stars: 0
    }
  },
  methods: {
    generateRandomNumber () {
      this.stars = Math.floor(Math.random() * (10 - 1 +1) + 1 )
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
  margin-top: 200px;
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

#answer-section {
  margin: 40px 0;
  background-color: lightblue;
  width: 5%;
  margin: auto;
  padding: 15px;
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
