<template>
  <div class="question-box-container">
    <b-jumbotron>
      <p>Question: {{ questionNum }} / 10</p>
      <h3>
        {{ currentQuestion.question | charTransform}}
      </h3>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          @click="selectAnswer(index)"
          :class="answerClass(index)"
        >
          {{ answer | charTransform }}
        </b-list-group-item>
      </b-list-group>

      <b-button
        variant="primary"
        @click="submitAnswer"
        :disabled="selectedIndex === null || answered"
      >
        Submit
      </b-button>
      <b-button
        @click="next(); addNum();"
        variant="success"
        :disabled="questionNum === 10"
      >
        Next
      </b-button>
      <p
        v-if="questionNum === 10"
        class="mt-4"
      >
        End of category quiz<br>
        Choose a different category
      </p>
    </b-jumbotron>
  </div>
</template>

<script>
  import _ from 'lodash'

  export default {
    props: {
      currentQuestion: Object,
      next: Function,
      increment: Function,
      charTransform: Function,
      questionNum: Number,
      addNum: Function
    },
    data() {
      return {
        selectedIndex: null,
        correctIndex: null,
        shuffledAnswers: [],
        answered: false
      }
    },
    computed: {
      answers() {
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)
        return answers
      }
    },
    watch: {
      currentQuestion: {
        immediate: true,
        handler() {
          this.selectedIndex = null
          this.answered = false
          this.shuffleAnswers()
        }
      }
    },
    methods: {
      selectAnswer(index) {
        this.selectedIndex = index
      },
      submitAnswer() {
        let isCorrect = false

        if (this.selectedIndex === this.correctIndex) {
          isCorrect = true
        }
        this.answered = true

        this.increment(isCorrect)
      },
      shuffleAnswers() {
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
        this.shuffledAnswers = _.shuffle(answers)
        this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
      },
      answerClass(index) {
        let answerClass = ''

        if (!this.answered && this.selectedIndex === index) {
          answerClass = 'selected'
        } else if (this.answered && this.correctIndex === index) {
          answerClass = 'correct'
        } else if (this.answered && this.selectedIndex === index && this.correctIndex !== index) {
          answerClass = 'incorrect'
        }
        return answerClass
      }
    },
    filters: {
      charTransform: (html) => {
        let txt = document.createElement('textarea')
        txt.innerHTML = html
        return txt.value
      }
    }
  }
</script>

<style lang='css' scoped>
  .question-box-container {
    margin-top: 30px;
    color: #0d0d0d;
  }
  .jumbotron {
    background-color: rgba(255,255,255,0.7);
    padding: 30px;
  }
  .list-group {
    margin-bottom: 15px;
  }
  .list-group-item {
    background-color: rgba(255,255,255,0.3);
  }
  .list-group-item:hover {
    background: rgba(255,255,255,0.5);
    cursor: pointer;
  }
  .selected {
    background-color: lightblue;
  }
  .correct {
    background-color: lightgreen;
  }
  .incorrect {
    background-color: lightcoral;
  }
  .btn {
    width: 100px;
    margin: 0 5px;
  }
</style>
