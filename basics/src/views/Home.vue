<template>
  <div class="container">
    <h1>Welcome to this Quiz Game!</h1>
    <h1 v-if="started"> {{ quiz[QuestionN].question }}</h1>
    <button v-if="started === true && clickable === true" v-on:click="checkAnswer"> {{ choices[0] }} </button>
    <button v-else-if="started === true"> {{ choices[0] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ choices[1] }} </button>
    <button v-else-if="started === true"> {{ choices[1] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ choices[2] }} </button>
    <button v-else-if="started === true"> {{ choices[2] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ choices[3] }} </button>
    <button v-else-if="started === true"> {{ choices[3] }} </button>
    <button v-on:click="startedQuiz" v-else>Begin</button>
    <button v-on:click="nextQuestion" v-if="submit">Submit</button>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  data() {
    return {
      quiz: [],
      choices: [],
      correct: {},
      correct_answer: {},
      last_correct_choice: {},
      QuestionN: 0,
      started: false,
      submit: false,
      clickable: false,
    };
  },
  methods: {
    startedQuiz: function() {
      this.started = true;
      this.clickable = true;
      this.correct_answer = 0;
      this.correct = this.quiz[this.QuestionN].correct_answer;
      this.choices = [this.correct, this.quiz[this.QuestionN].incorrect_answers[0], this.quiz[this.QuestionN].incorrect_answers[1], this.quiz[this.QuestionN].incorrect_answers[2]];
    },
    checkAnswer: function() {
      this.last_correct_choice = this.correct_answer;
      this.submit = true;
      this.clickable = false;
    },
    shuffle: function (array) {
      for (let i = array.length - 1; i > 0; i--) {
        var j = (Math.round(Math.random() * 3));
        var temp = array[i];
        array[i] = array[j];
        array[j] = temp;
      }
    },
    nextQuestion: function () {
      this.submit = false;
      this.clickable = true;
      this.QuestionN ++;
      this.correct = this.quiz[this.QuestionN].correct_answer;
      this.choices = [this.correct, this.quiz[this.QuestionN].incorrect_answers[0], this.quiz[this.QuestionN].incorrect_answers[1], this.quiz[this.QuestionN].incorrect_answers[2]];
      this.shuffle(this.choices);
      console.log(this.quiz[this.QuestionN].correct_answer); 
    },
    fetchData: async function() {
      try {
        const result = await fetch (`https://opentdb.com/api.php?amount=10&category=23&difficulty=medium&type=multiple`);
        const data = await result.json();
        console.log(data);
        this.quiz = data.results;    
      }
      catch(error) {
        alert(error);
      }
    },
    
  },
  created() {
    
  },
  mounted() {  
        this.fetchData();
  },
  beforeCreate() {},
};
</script>

<style lang="scss" scoped>
h1 {
  font-size: 3rem;
}
button {
  font-size: 2rem;
}
</style>