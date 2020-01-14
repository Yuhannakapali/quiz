<template>


 <div class="question-box-container">
  <b-jumbotron >
    <template v-slot:lead>
     {{currentQuestion.question}}
    </template>

    <hr class="my-4">

    
      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index" 
          @click="selectanswer(index)"
          :class="[selectedIndex === index ? 'selected' : '']"
        >
          {{ answer }}

        </b-list-group-item>
      
      </b-list-group>
    

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
  data(){
    return {
      selectedIndex: null
    }
  },
  computed: {
    answers(){
      let answers = [...this.currentQuestion.incorrect_answers]
      answers.push(this.currentQuestion.correct_answer)
      return answers
    }
  },
  watch:{
    currentQuestion(){
      this.selectedIndex= null
      
    }
  },
  methods: {
    selectanswer(index){
      this.selectedIndex= index
      console.log(index)
    }
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