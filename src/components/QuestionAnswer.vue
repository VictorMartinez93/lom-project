<template>
  <div class="wrapper-questions">
    <div class="header"></div>
    <div class="question-answer" v-for="(qa, index) in qas" :key="qa">
      <div class="wrapper-question-answer" v-if="index === this.questionNumber">
        <h3>{{ qa.question }}</h3>
        <div class="user-answer">
          <!-- Text & Number input -->
          <div v-if="qa.type === 'text' || qa.type === 'number'">
            <input
              :type="qa.type"
              :disabled="qa.answered"
              v-model="qa.userAnswer"
              @change="onChangeTextNumber(qa)"
            />
          </div>

          <!-- Radio input -->
          <div v-if="qa.type === 'radio'" class="wrapper-line">
            <div class="btn-group" v-for="option in qa.options" :key="option">
              <label
                class="btn btn-lg"
                :class="[
                  option.selected && qa.userAnswer === qa.answer
                    ? 'btn-correct'
                    : '',
                  option.selected && qa.userAnswer !== qa.answer
                    ? 'btn-wrong'
                    : '',
                  qa.answered ? 'btn-disabled' : '',
                ]"
              >
                <input
                  type="radio"
                  hidden
                  :value="option.value"
                  name="questionOption"
                  @change="onChangeRadio(option, qa)"
                  :disabled="qa.answered"
                />
                {{ option.value }}
              </label>
            </div>
          </div>
        </div>
        <div class="feedback" v-if="qa.answered">
          <p :class="[qa.correct ? 'correct-answer' : 'wrong-answer']">
            <span v-if="qa.correct">Correct!!</span>
            <span v-if="!qa.correct"
              >Sorry!! the answer is: {{ qa.answer }}</span
            >
          </p>
        </div>
        <div class="wrapper-buttons">
          <div class="wrapper-navigation" v-if="qa.answered">
            <button
              type="button"
              class="btn btn-light"
              v-if="this.questionNumber > 0"
              @click="previousQuestion()"
            >
              Previous
            </button>
            <button
              v-if="this.questionNumber < this.qas.length - 1"
              type="button"
              class="btn btn-primary"
              @click="nextQuestion()"
            >
              Next
            </button>
            <button
              v-if="this.questionNumber === this.qas.length - 1"
              type="button"
              class="btn btn-success"
              @click="endQuiz()"
            >
              End quiz
            </button>
          </div>
          <div class="wrapper-check" v-if="!qa.answered && qa.type !== 'radio'">
            <!-- <button type="button" class="btn btn-success">Check answer</button> -->
            <p class="text-muted italics">
              To check the answer press enter or click outside the box.
            </p>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">{{ this.questionNumber + 1 }}/{{ qas.length }}</div>
  </div>
</template>
<script>
export default {
  name: "QuestionAnswer",
  props: {
    qas: Array,
  },
  data() {
    return {
      questionNumber: 0,
    };
  },
  methods: {
    previousQuestion() {
      this.questionNumber--;
    },
    nextQuestion() {
      this.questionNumber++;
    },
    endQuiz() {
      this.$emit("show-summary");
    },
    onChangeTextNumber(qa) {
      if (qa.type === "text") {
        qa.correct = qa.userAnswer.toLowerCase() === qa.answer.toLowerCase();
      } else {
        qa.correct = qa.userAnswer === qa.answer;
      }
      qa.answered = true;
    },
    onChangeRadio(option, qa) {
      qa.userAnswer = option.value;
      option.selected = true;
      qa.answered = true;
      qa.correct = qa.userAnswer === qa.answer;
    },
  },
  emits: ["show-summary"],
};
</script>
<style scoped>
.wrapper-questions {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.wrapper-question-answer {
  min-height: 250px;
}

.user-answer {
  margin-top: 2rem;
}

.wrapper-line,
.wrapper-navigation {
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 1rem;
}

.wrapper-buttons {
  margin-top: 2rem;
}

input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.correct-answer {
  color: #087208;
}

.wrong-answer {
  color: #972929;
}

.footer {
  display: block;
  position: absolute;
  bottom: 1rem;
}
</style>