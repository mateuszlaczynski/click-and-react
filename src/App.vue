
<template>
  <h1>Przetestuj swój czas reakcji!</h1>
  <p>Po wciśnięciu przycisku "Start!" zaczekaj aż poniższe pole
     zmieni kolor na zielony, następnie kliknij na nie.</p>
  <br>
  <button :disabled="buttonDisabled" @click="startGame">Start!</button>
  <div v-if="boxActive" class="box">
    <div id="box-text">
        <div v-if="score > 0"> 
          <h4>Twój wynik: {{score}}s</h4>
          <p style="color:darkcyan;" v-if="score < 1 && score >= 0.1">Dobry wynik!</p>
          <p style="color:red;" v-else>Spróbuj ponownie!</p>

        </div>
        
    </div>
    
  </div>
  <div v-else class="box-click" @click="stopGame">
    <div id="box-text">
      <h2>Kliknij teraz!</h2>
    </div>
    
  </div>

</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      buttonDisabled: false,
      boxActive: true,
      counter: 0.0,
      score: 0.0,
      intervalId: '',
    }
  },
  methods: {
    timeCounter() {
      this.counter += 0.01
    },
    startGame() {
      this.score = 0
      this.buttonDisabled = true
      setTimeout(() => {
        this.boxActive = false; 
        this.intervalId = setInterval((this.timeCounter), 10)
      }, Math.random()*10000)
      
  },
    stopGame() {
      clearInterval(this.intervalId)
      this.buttonDisabled = false
      this.boxActive = true
      this.score = this.counter.toFixed(2)
      this.counter = 0
    }
  },
}
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
h1 {
  border-bottom: solid 1px darkcyan;
  display: inline-block;
}
button {
  width:100px;
  padding:10px;
  background-color:darkcyan;
  color: white;
  border: 1px solid;
  border-radius: 10%;
  border-color: black;
}
button:hover {
  background-color: white;
  border-radius: 10%;
  padding:10px;
  color: darkcyan;
  cursor:pointer;
}
button:disabled {
  background-color:lightgray;
  border-radius: 10%;
  padding:10px;
  color: gray;
  cursor: auto;
  border: 1px solid;
  border-color: white;
}
.box {
  background-color: white;
  width: 500px;
  height: 300px;
  margin: 30px;
  margin-left: auto;
  margin-right: auto;
  border-radius: 10%;
  border: solid 1px lightgray
}
.box-click {
  background-color: darkcyan;
  width: 500px;
  height: 300px;
  margin: 30px;
  margin-left: auto;
  margin-right: auto;
  border-radius: 10%;
  border: solid 1px lightgray;
  color: white;
  cursor: pointer;
}
#box-text {
  top: 50%;
  left: 50%;
  margin-top: 120px;
}
</style>
