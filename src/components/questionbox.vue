<template>


 <div class="question-box-container">
  <b-jumbotron >
    <template v-slot:lead>
     {{currentQuestion.question}}
    </template>

    <hr class="my-4">

    
      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers "
          :key="index" 
          @click="selectanswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}

        </b-list-group-item>
      
      </b-list-group>
    

    <b-button
    variant="primary" 
    @click="submitAnswer"
    :disabled="selectedIndex === null || answered "
    >
    
    submit
    </b-button>
    <b-button
     @click="next" 
     variant="success" 
     href="">
     Next

    </b-button>
  </b-jumbotron>
</div>
</template>

<script>
import  _  from 'lodash' 


export default {
  
 
  props:{
    currentQuestion: Object,
    next : Function,
    increment: Function

  },
  data(){
    return {
      selectedIndex: null,
      shuffledAnswers : [],
      correctIndex: null,
      answered: false
    }
  },
  computed: {
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch: {
    currentQuestion :{
      immediate: true,
      handler(){
      this.selectedIndex= null
      this.answered= false
        this.shuffleAnswers()
      }
    }
    
    
    // () {
    //   this.selectedIndex= null
    //   this.shuffleAnswers()

    // }
  },
  methods: {
    selectanswer(index){
      this.selectedIndex= index
      console.log(index)
    },

    submitAnswer(){
      let isCorrect=false

      if (this.selectedIndex === this.correctIndex) {
        console.log(this.correctIndex)
        isCorrect = true
      }
      this.answered = true
      this.increment(isCorrect)
    },

    shuffleAnswers() {
      let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
      this.shuffledAnswers = _.shuffle(answers)
     this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    }
    // suffleAnswer(){
    //   let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
    //   this.suffledAnswers = _.shuffle(answers)
     
    // }
  }
    

}
</script>

<style  scoped>
.list-group{
  margin-bottom : 15px;
}
.list-group-item:hover{
  background: #eee;
}


.btn{
  margin: 0 5px;
}

.selected {
  background: lightblue;
}
.correct{
  background: lightgreen;

}

.incorrect{
  background: red;
}
</style>