<template>
  <div>
    <h3>Correct questions: {{ correctQuestions }}</h3>
  </div>
  <div>
    <h3>Nº of questions: {{ numberOfQuestions }}</h3>
  </div>
  <div>
    <div v-if="correctQuestions < numberOfQuestions / 3" class="fatal-summary">
      Are you joking me? 🤔 This is why you deserve an extinction 😡
    </div>
    <div
      v-if="
        correctQuestions >= numberOfQuestions / 3 &&
        correctQuestions <= numberOfQuestions / 2
      "
      class="medium-summary"
    >
      Not bad not bad, but you are not worth of this anyway. 🙃
    </div>
    <div v-if="correctQuestions > numberOfQuestions / 2" class="great-summary">
      You proved your worthiness... but I'm not as kind as you think, I'm here
      to extinct you. 🙂
    </div>
  </div>
</template>
<script>
export default {
  name: "Summary",
  props: {
    correctQuestions: Number,
    numberOfQuestions: Number,
  },
};
</script>
<style>
</style>