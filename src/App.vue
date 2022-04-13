<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz App</h1>
      </div>
      <div class="quiz-main" v-for="(element, index) in questions.slice(a, b)" :key="index" v-show="quiz">
        <div class="box-question">
          <h2>Question {{ b }} / {{ questions.length }}</h2>
          <p>{{ element.question }}</p>
        </div>
        <div class="box-suggestions">
          <ul>
            <li v-for="(item, index) in element.suggestions" :key="index" :class="select ? check(item) : ''" @click="selectResponse(item)">{{ item.suggestion }}</li>
          </ul>
        </div>
      </div>
      <div class="quiz-footer">
        <div class="box-button">
          <button @click="skipQuestion">Skip</button>
          <button @click="nextQuestion">Next</button>
        </div>
      </div>
      <div class="box-score" v-if="score_show">
        <h2>Your score is</h2>
        <h2>{{ score }}/{{ questions.length }}</h2>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      questions: [
        {
          question: 'Question 1',
          suggestions: [
            {suggestion: 'Suggestion 1'},
            {suggestion: 'Suggestion 2'},
            {suggestion: 'Suggestion 3', correct: true},
            {suggestion: 'Suggestion 4'},
          ]
        },
        {
          question: 'Question 2',
          suggestions: [
            {suggestion: 'Suggestion 1'},
            {suggestion: 'Suggestion 2', correct: true},
            {suggestion: 'Suggestion 3'},
            {suggestion: 'Suggestion 4'},
          ]
        },
        {
          question: 'Question 3',
          suggestions: [
            {suggestion: 'Suggestion 1'},
            {suggestion: 'Suggestion 2'},
            {suggestion: 'Suggestion 3'},
            {suggestion: 'Suggestion 4', correct: true},
          ]
        },
        {
          question: 'Question 4',
          suggestions: [
            {suggestion: 'Suggestion 1', correct: true},
            {suggestion: 'Suggestion 2'},
            {suggestion: 'Suggestion 3'},
            {suggestion: 'Suggestion 4'},
          ]
        },
      ],
      a: 0,
      b: 1,
      select: false,
      score: 0,
      quiz: true,
      score_show: false,
    }
  },
  methods: {
    selectResponse(e) {
      this.select = true;
      if(e.correct){
        this.score++;
      }
    },
    check(status){
      if(status.correct){
        return 'correct';
      } else {
        return 'incorrect';
      }
    },
    nextQuestion() {
      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;
      }else{
        this.a++;
        this.b++;
        this.select = false;
      }
    },
    skipQuestion(){
      if(this.questions.length - 1 == this.a){
        this.score_show = true;
        this.quiz = false;
      }else{
        this.a++;
        this.b++;
      }
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
