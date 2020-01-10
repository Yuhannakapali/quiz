<template>
  <div id="app">
   
    <top />
    <b-container class="bv-example-row">
  <b-row>
    <b-col sm-6 >
      <questionbox 
        v-if="question.length"
        :currentQuestion = "question[index]"
        v-on:next = "nexthandler"


      />
        
    </b-col>
    
  </b-row>
</b-container>
    
  </div>
</template>

<script>

import top from './components/top.vue'
import questionbox from './components/questionbox.vue'
//import Nav from './components/nav.vue'

export default {
  
    
  name: 'app',

 
  components: {
    top,
    questionbox
  },
  data(){
   return{
     question : [],
     index : 0
   }
  },
  methods:{
    nexthandler() {
      //this.console.log("here");
      this.index++
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=31&difficulty=easy&type=multiple',{
      method: 'get'
    })

    .then ((response)=>{
      return response.json()
    })

    .then((jsonData)=>{
      this.question = jsonData.results
    })

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
  margin-top: 60px;
}
</style>
