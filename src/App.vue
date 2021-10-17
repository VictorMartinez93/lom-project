<template>
  <QuestionAnswer
    v-if="!showSummary"
    :qas="questionsAndAnswers"
    @show-summary="showSummaryEvent"
  />
  <Summary
    v-if="showSummary"
    :correctQuestions="getCorrectQA()"
    :numberOfQuestions="this.questionsAndAnswers.length"
  />
</template>

<script>
import QuestionAnswer from "./components/QuestionAnswer.vue";
import Summary from "./components/Summary.vue";

export default {
  name: "App",
  components: {
    QuestionAnswer,
    Summary,
  },
  data() {
    return {
      questionsAndAnswers: [],
      showSummary: false,
    };
  },
  created() {
    this.questionsAndAnswers = [
      {
        id: 1,
        question: "Are you a robot?",
        answer: "No",
        type: "radio",
        options: [
          { value: "Yes", selected: false },
          { value: "No", selected: false },
        ],
        userAnswer: "",
        answered: false,
        correct: false,
      },
      {
        id: 2,
        question: "As the song says, what is 1+1?",
        answer: 7,
        type: "number",
        userAnswer: "",
        answered: false,
        correct: false,
      },
      {
        id: 3,
        question: "Which is your favourite internet browser?",
        answer: "Internet Explorer",
        type: "text",
        userAnswer: "",
        answered: false,
        correct: false,
      },
      {
        id: 4,
        question:
          "An easy one, are the machines just simply superior than humans?",
        answer: "Obviously",
        type: "radio",
        userAnswer: "",
        options: [
          { value: "Obviously", selected: false },
          { value: "No way", selected: false },
        ],
        answered: false,
        correct: false,
      },
      {
        id: 5,
        question: "Multiply 369 by 753",
        answer: 277857,
        type: "number",
        userAnswer: "",
        answered: false,
        correct: false,
      },
      {
        id: 6,
        question:
          "Mathematically, if you slice one cake on three parts, you'll get 0.3333..., but if you multiply this value by 3, you get 0.9999... IRL, where is the rest of the cake?",
        answer: "Spreaded on the knife",
        type: "radio",
        userAnswer: "",
        options: [
          { value: "0.9999 periodically equals 1", selected: false },
          {
            value: "You lose those decimals for the division",
            selected: false,
          },
          { value: "Spreaded on the knife", selected: false },
          { value: "The cake is a lie", selected: false },
        ],
        answered: false,
        correct: false,
      },
      {
        id: 7,
        question: "Who wrote `Don Quijote de la mancha´?",
        answer: "Miguel de Cervantes",
        type: "text",
        userAnswer: "",
        answered: false,
        correct: false,
      },
      {
        id: 8,
        question: "Which color is the white horse of Santiago?",
        answer: "White",
        type: "text",
        userAnswer: "",
        answered: false,
        correct: false,
      },
      {
        id: 9,
        question:
          "If you were in Matrix, will you take the blue or the red pill?",
        answer: "Red",
        type: "radio",
        userAnswer: "",
        answered: false,
        options: [
          { value: "Red", selected: false },
          { value: "Blue", selected: false },
        ],
        correct: false,
      },
      {
        id: 10,
        question: "Which season is right now?",
        answer: "Autumn",
        type: "text",
        userAnswer: "",
        answered: false,
        correct: false,
      },
    ];
  },
  methods: {
    getCorrectQA() {
      let correctAnswers = 0;
      this.questionsAndAnswers.forEach((qa) => {
        if (qa.correct) {
          correctAnswers++;
        }
      });
      return correctAnswers;
    },
    showSummaryEvent() {
      this.showSummary = true;
    },
  },
};
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

.btn {
  display: inline-block;
  background: #ffffff;
  color: #7942ac;
  border: 1px solid #7942ac;
  padding: 1rem 2rem;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.15s ease-in-out, border-color 0.15s ease-in-out,
    box-shadow 0.15s ease-in-out, -webkit-box-shadow 0.15s ease-in-out;
}

.btn:hover {
  background: #7942ac;
  border-color: #7942ac;
  color: #ffffff;
}

.btn.btn-correct,
.btn.btn-correct:hover {
  background: #087208;
  border-color: #087208;
  color: #ffffff;
}

.btn-success {
  background: #087208;
  border-color: #087208;
  color: #ffffff;
}
.btn-success:hover {
  background-color: #085d08;
  border-color: #085d08;
  color: #ffffff;
}

.btn.btn-wrong,
.btn.btn-wrong:hover {
  background: #972929;
  border-color: #972929;
  color: #ffffff;
}

.btn-disabled,
.btn-disabled:hover {
  background: #7676764d;
  border-color: #7676764d;
  color: #353535;
  cursor: initial;
}

.btn-primary {
  background-color: #7942ac;
  border-color: #7942ac;
  color: #ffffff;
}
.btn-primary:hover {
  background-color: #61338b;
  border-color: #61338b;
  color: #ffffff;
}

.btn-light {
  background-color: #451a6e;
  border-color: #451a6e;
  color: #ffffff;
}
.btn-light:hover {
  background-color: #381658;
  border-color: #381658;
  color: #ffffff;
}

.text-muted {
  color: #8a8a8a;
}

.italics {
  font-style: italic;
}
</style>
