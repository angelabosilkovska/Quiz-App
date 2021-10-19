<template>
  <div>
  <b-nav tabs>
    <b-nav-item disable><b>Quiz App</b></b-nav-item>
    <b-nav-item disablel>Counter: {{ numCorrect }}/{{ numTotal }}</b-nav-item>
  </b-nav>
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

<style scoped>
.nav-tabs{
margin-top: 0px;  
margin-bottom: 25px;
}
</style>