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
      v-if="!showScore"
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
     />
     <Score
     v-else
     :numCorrect="numCorrect"
     :numTotal="numTotal"
     :playagain="playagain"
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
  computed:{
    showScore(){
      if (this.index === this.questions.length) {
        return true
      }else{
        return false
      }
    }
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
    playagain(type){
      this.fetchQuestions(type)
      this.index= 0;
      this.numCorrect= 0;
      this.numTotal= 0;
    },
   async fetchQuestions(type){
    await fetch(`https://opentdb.com/api.php?amount=10&category=${type}&type=multiple`, {
      method: 'get'
    })
    .then((response) => {
      return response.json()
    })
    .then((jsonData) => {
      this.questions = jsonData.results
      console.log('prasanja',this.questions);
    })
    },
    next() {
      this.index++
      console.log(this.index);
      console.log(this.showScore);
    },
    increment(isCorrect){
      if (isCorrect){
      this.numCorrect++
    }
     this.numTotal++
    }
  },
  mounted: function() {
      this.fetchQuestions(21)
  }
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
</style>
