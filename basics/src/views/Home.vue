<template>
  <div class="container">
    <h1>Welcome to this Quiz Game!</h1>
    <h1 v-if="started && finish === false"> {{ quiz[QuestionN].question }}</h1>
    <button v-if="started === true && clickable === true && finish === false" v-on:click="checkAnswer(choices[0])"> {{ choices[0] }} </button>
    <button v-else-if="started === true && finish === false" > {{ choices[0] }} </button>
    <button v-if="started && clickable === true && finish === false" v-on:click="checkAnswer(choices[1])"> {{ choices[1] }} </button>
    <button v-else-if="started === true && finish === false"> {{ choices[1] }} </button>
    <button v-if="started && clickable === true && finish === false" v-on:click="checkAnswer(choices[2])"> {{ choices[2] }} </button>
    <button v-else-if="started === true && finish === false"> {{ choices[2] }} </button>
    <button v-if="started && clickable === true && finish === false" v-on:click="checkAnswer(choices[3])"> {{ choices[3] }} </button>
    <button v-else-if="started === true && finish === false"> {{ choices[3] }} </button>
    <button v-on:click="startedQuiz" v-else-if="finish === false">Begin</button>
    <button v-on:click="nextQuestion" v-if="submit === true && finish === false">Submit</button>
    <button v-on:click="nextQuestion" v-if="done === true">Finish</button>
    <button v-on:click="startedQuiz" v-if="finish === true">Finish</button>
    <h1 v-if="finish"> {{ correct }} / 10</h1>

  </div>
</template>

<script>
// @ is an alias to /src
export default {
  data() {
    return {
      quiz: [],
      choices: [],
      QuestionN: 0,
      started: false,
      submit: false,
      clickable: false,
      done: false,
      finish: false,
      correct: 0,
    };
  },
  methods: {
    startedQuiz: function() {
      this.fetchData;
      this.started = true;
      this.clickable = true;
      this.done = false;
      this.finish = false;
      this.QuestionN = 0;
      this.correct = 0;
      this.choices = [this.quiz[this.QuestionN].correct_answer, this.quiz[this.QuestionN].incorrect_answers[0], this.quiz[this.QuestionN].incorrect_answers[1], this.quiz[this.QuestionN].incorrect_answers[2]];
    },
    checkAnswer: function(answer) {
      if (this.QuestionN === 9) {
        this.submit = true;
      this.clickable = false;
      } else {
      this.submit = true;
      this.clickable = false;
      }

      if (answer === this.quiz[this.QuestionN].correct_answer) {
        this.correct ++;
      }
    },
    shuffle: function (array) {
      for (let i = array.length - 1; i > 0; i--) {
        var j = (Math.round(Math.random() * 3 - 0.25));
        var temp = array[i];
        array[i] = array[j];
        array[j] = temp;
        this.choices = [array[0], array[1], array[2], array[3]]
      }
    },
    nextQuestion: function () {
      if (this.QuestionN === 9) {
        this.finish = true;
        this.done = false;
      } else {
      this.submit = false;
      this.clickable = true;
      this.QuestionN ++;
      this.choices = [this.quiz[this.QuestionN].correct_answer, this.quiz[this.QuestionN].incorrect_answers[0], this.quiz[this.QuestionN].incorrect_answers[1], this.quiz[this.QuestionN].incorrect_answers[2]];
      this.shuffle(this.choices);
      }
    },
    fetchData: async function() {
      try {
        const result = await fetch (`https://opentdb.com/api.php?amount=10&category=23&difficulty=medium&type=multiple`);
        const data = await result.json();
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