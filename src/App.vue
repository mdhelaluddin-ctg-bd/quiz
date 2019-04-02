<template>
  <div id="app">
    <HeaderComponent
      v-if="questions.length"
      :totalQuestion="questions.length"
      :currentQuestion="index+1"
      :noOfCorrectAnswer="noOfCorrectAnswer"
    />
    <b-container>
      <QuestionBoxComponent 
      v-if="questions.length" 
      :currentQuestion="questions[index]" 
      :totalQuestion="questions.length"
      :index="index+1"
      :next="next"
      :startNewQuiz="startNewQuiz"
      :increaseCorrectAnswer="increaseCorrectAnswer" />
      
    </b-container>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent.vue'
import QuestionBoxComponent from './components/QuestionBoxComponent'


export default {
  name: 'app',
  components: {
    HeaderComponent,
    QuestionBoxComponent,
    
  },
  data () {
    return {
      questions : [],
      index: 0,
      noOfCorrectAnswer : 0,
      loading : true
    }
  },
  mounted: function() {
    this.setInitialData()
  },
  methods : {
    next () {
      this.index++;
    },
    increaseCorrectAnswer() {
      this.noOfCorrectAnswer++;
    }, 
    startNewQuiz() {
      this.setInitialData();
    },
    setInitialData() {

      
      fetch('https://opentdb.com/api.php?amount=10&difficulty=medium&type=multiple')
      .then((response) => {
        return response.json();
      })
      .then((jsonData) => {
        this.questions = jsonData.results
        
        // Initial Values
        this.index = 0;
        this.noOfCorrectAnswer = 0;
      });
    }
  }
  
}

</script>


