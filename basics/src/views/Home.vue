<template>
  <div class="container">
    <h1>Welcome to this Quiz Game!</h1>
    <h1 v-if="started"> {{ quiz[QuestionN].question }}</h1>
    <button v-if="started === true && clickable === true" v-on:click="checkAnswer"> {{ quiz[QuestionN].correct_answer }} </button>
    <button v-else-if="started === true"> {{ quiz[QuestionN].correct_answer }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ quiz[QuestionN].incorrect_answers[0] }} </button>
    <button v-else-if="started === true"> {{ quiz[QuestionN].incorrect_answers[0] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ quiz[QuestionN].incorrect_answers[1] }} </button>
    <button v-else-if="started === true"> {{ quiz[QuestionN].incorrect_answers[1] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ quiz[QuestionN].incorrect_answers[2] }} </button>
    <button v-else-if="started === true"> {{ quiz[QuestionN].incorrect_answers[2] }} </button>
    <button v-on:click="startedQuiz" v-else>Begin</button>
    <button v-on:click="nextQuestion" v-if="submit">Submit</button>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home",
  components: {},
  data() {
    return {
      quiz: [],
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
    },
    checkAnswer: function() {
      this.submit = true;
      this.clickable = false;
    },
    nextQuestion: function () {
      this.submit = false;
      this.clickable = true;
      this.QuestionN ++;
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