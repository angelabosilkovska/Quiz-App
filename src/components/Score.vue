<template>
  <div>
    <b-jumbotron>
        <h1>Your final score is:</h1>
        <br>
        <h2>{{ numCorrect }}/{{ numTotal }}</h2>
           <b-form-group label="Select category!" v-slot="{ ariaDescribedby }">
      <b-form-radio v-model="selected" :aria-describedby="ariaDescribedby" name="some-radios" value="27">ANIMAL</b-form-radio>
      <b-form-radio v-model="selected" :aria-describedby="ariaDescribedby" name="some-radios" value="21">SPORT</b-form-radio>
    </b-form-group>
        <b-button @click="playagain(selected)">
            Play Again
        </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
     props: [
    'numCorrect',
    'numTotal',
    'playagain'
  ],
     data() {
      return {
        selected: ''
      }
    }
}
</script>

<style>

</style>