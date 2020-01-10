<template>


 <div class="question-box-container">
  <b-jumbotron >
    <template v-slot:lead>
     {{currentQuestion.question}}
    </template>

    <hr class="my-4">

     <!-- <p v-for="(answer, index) in answers" :key="index">
     {{answers}} 

    </p> -->

    <b-button variant="primary" href="#">submit</b-button>
    <b-button @click="$emit('next')" variant="success" href="">next</b-button>
  </b-jumbotron>
</div>
</template>

<script>
export default {
  props:{
    currentQuestion: Object,
    next : Function
  },
  computed: {
    answers(){
      let answers = [...this.currentQuestion.incorrect_answer]
      return answers.push(this.currentquestion.correct_answer)
    }
  }
    

}
</script>