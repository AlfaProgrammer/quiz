<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <QuestionsComponent
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @verify-answer="verifyAnswer"
      />
      <ResultsComponent
        v-else
        :correctAnswers="correctAnswers"
        :results="results"
      />
    </transition>

    <button 
      type="button" 
      class="reset-btn" 
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>

  </div>
</template>

<script>

import QuestionsComponent from './components/QuestionsComponent.vue'
import ResultsComponent from './components/ResultsComponent.vue'

export default {
  name: 'App',
  components: {
    QuestionsComponent,
    ResultsComponent
  },
  data(){
    return{
      questionsAnswered: 0,
      correctAnswers: 0,
      questions: [
        {
          q: "What is 2 + 2",
          answers:[
            {
              text: "4",
              is_correct: true,
            },
            {
              text: "3",
              is_correct: false,
            },
            {
              text: "8",
              is_correct: false,
            },
            {
              text: "5",
              is_correct: false,
            },
          ]
        },
        {
          q: "Find the missing letter: C_t",
          answers: [
            {
              text: "e",
              is_correct: false
            },
            {
              text: "a",
              is_correct: true
            },
            {
              text: "b",
              is_correct: false
            },
            {
              text: "k",
              is_correct: false
            },
          ]
        },
        {
          q: "Haw many letters are in the word 'Banana' ? ",
          answers: [
            {
              text: '5',
              is_correct: false
            },
            {
              text: '3',
              is_correct: false
            },
            {
              text: '6',
              is_correct: true
            },
            {
              text: '8',
              is_correct: false
            },
          ]
        }
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again",
          desc: "Do a little more studying and you will succeed!"
        },
        {
          min: 3,
          max: 3,
          title: "You are a genius",
          desc: "Studying has definitely paid off for you!"
        },
      ]
    }
  },
  methods:{
    verifyAnswer(is_correct){
      if(is_correct){
        this.correctAnswers++
      }

      this.questionsAnswered++
    },
    reset(){
      this.questionsAnswered = 0
      this.correctAnswers = 0
    }
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
