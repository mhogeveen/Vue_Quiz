<template>
  <div id="app">
    <Header
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />
    <Category
      :urls="urls"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Category from './components/Category.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    Category,
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0,
      urls: [
        {
          name: 'Animals',
          url: 'https://opentdb.com/api.php?amount=10&category=27&type=multiple'
        },
        {
          name: 'Mythology',
          url: 'https://opentdb.com/api.php?amount=10&category=20&type=multiple'
        },
        {
          name: 'Art',
          url: 'https://opentdb.com/api.php?amount=10&category=25&type=multiple'
        },
        {
          name: 'Sports',
          url: 'https://opentdb.com/api.php?amount=10&category=21&type=multiple'
        },
        {
          name: 'Science & Nature',
          url: 'https://opentdb.com/api.php?amount=10&category=17&type=multiple'
        }
      ]
    }
  },
  methods: {
    next() {
      this.index++
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
    },
    pickCategory() {
      
    }
  },
  mounted: function() {
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
      method: 'get'
    })
    .then((response) => {
      return response.json()
    })
    .then((jsonData) => {
      this.questions = jsonData.results
    })
  }
}
</script>

<style>
#app {
  font-family: Montserrat, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0d0d0d;
}
</style>
