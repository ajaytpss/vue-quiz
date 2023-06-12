<template>
  <div class="ctr">
    <div class="questions-ctr">
      <div class="progress">
        <div class="bar"></div>
        <div class="status">
          {{ answered }} out of {{ questions.length }} questions answered
        </div>
      </div>
      <div class="single-question">
        <div class="question">{{ questions[currentQus].q }}</div>
        <div class="answers">
          <div
            class="answer"
            @click="quizHandler(ans.is_correct)"
            v-for="ans in questions[currentQus].answers"
          >
            {{ ans.text }}
          </div>
        </div>
      </div>
    </div>
    <template v-if="answered === questions.length">
      <div class="result" v-if="trueAnswers > 2">
        <div class="title">{{ results[1].title }}</div>
        <div class="desc">{{ results[1].desc }}</div>
      </div>
      <div class="result" v-else>
        <div class="title">{{ results[0].title }}</div>
        <div class="desc">{{ results[0].desc }}</div>
      </div>
    </template>
    <button type="button" @click="resetQuiz" class="reset-btn">Reset</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentQus: 0,
      answered: 0,
      answers: [],
      trueAnswers: 0,
      questions: [
        {
          q: "What is 2 + 2?",
          answers: [
            {
              text: "4",
              is_correct: true,
            },
            {
              text: "3",
              is_correct: false,
            },
            {
              text: "Fish",
              is_correct: false,
            },
            {
              text: "5",
              is_correct: false,
            },
          ],
        },
        {
          q: 'How many letters are in the word "Banana"?',
          answers: [
            {
              text: "5",
              is_correct: false,
            },
            {
              text: "7",
              is_correct: false,
            },
            {
              text: "6",
              is_correct: true,
            },
            {
              text: "12",
              is_correct: false,
            },
          ],
        },
        {
          q: "Find the missing letter: C_ke",
          answers: [
            {
              text: "e",
              is_correct: false,
            },
            {
              text: "a",
              is_correct: true,
            },
            {
              text: "i",
              is_correct: false,
            },
          ],
        },
        {
          q: "What is 2 + 6?",
          answers: [
            {
              text: "5",
              is_correct: false,
            },
            {
              text: "8",
              is_correct: true,
            },
            {
              text: "15",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Try again!",
          desc: "Do a little more studying and you may succeed!",
        },
        {
          min: 3,
          max: 3,
          title: "Wow, you're a genius!",
          desc: "Studying has definitely paid off for you!",
        },
      ],
    };
  },
  methods: {
    quizHandler(ans) {
      if (this.answered + 1 <= this.questions.length) {
        this.answered++;
        this.answers.push(ans);
      }
      if (this.currentQus + 1 < this.questions.length) {
        this.currentQus++;
      }
      if (this.answered == this.questions.length) {
        this.trueAnswers = this.answers.filter((val) => val === true).length;
      }
      console.log(this.trueAnswers);
    },
    resetQuiz() {
      this.currentQus = 0;
      this.answered = 0;
      this.trueAnswers = 0;
      this.answers = [];
    },
  },
};
</script>
