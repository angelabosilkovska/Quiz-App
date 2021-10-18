<template>
  <div v-show="index === questions.length">
    <b-jumbotron>
        <h1>Your final score is:</h1> 
        <br>
        <h2>{{ numCorrect }}/{{ numTotal }}</h2>

        <b-button>
            Play Again
        </b-button>    
    </b-jumbotron>
  </div>
</template>

<script>
export default {
     props: [
    'numCorrect',
    'numTotal'
  ]
}
</script>

<style>

</style>