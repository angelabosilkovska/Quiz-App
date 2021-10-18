<template>
  <div id="app">
    <Header 
    :numCorrect="numCorrect"
    :numTotal="numTotal"
    />

    <b-container class="bv-example-row">
    <b-row>
    <b-col sm="6" offset=3>
     <QuestionBox 
      v-if="questions.length"
      :currentQuestion="questions[index]" 
      :next="next"
      :increment="increment"
     />
     <Score 
     v-show="showScore"
     />
    </b-col>
    </b-row>
    </b-container>
    
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import Score from './components/Score.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    Score
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
    }
  },
  methods: {
    next() {
      this.index++
    },
    increment(isCorrect){
      if (isCorrect){
      this.numCorrect++
    }
    this.numTotal++
    },
    showScore(){
      let isShowing = false
    
      if (this.index === this.questions.length ) {

        isShowing = true
      }
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
      method: 'get'
    })
    .then((response) => {
      return response.json()
    })
    .then((jsonData) => {
      this.questions = jsonData.results
    })
  }
}
</script>

import "bootstrap/dist/css/bootstrap.min.css";
import "bootstrap-vue/dist/bootstrap-vue.css";
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
