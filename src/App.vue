<template>
  <div id="app">
    <Header
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />
    <Category
      :urls="urls"
      :pickCategory="pickCategory"
      :currentCategory="currentCategory"
      :resetNum="resetNum"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
            :questionNum="questionNum"
            :addNum="addNum"
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
      questionNum: 1,
      currentCategory: '',
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
        },
        {
          name: 'Geography',
          url: 'https://opentdb.com/api.php?amount=10&category=22&type=multiple'
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
    pickCategory(value) {
      let pickedUrl = this.urls[value].url
      fetch(pickedUrl, {
        method: 'get'
      })
      .then((response) => {
        return response.json()
      })
      .then((jsonData) => {
        this.questions = jsonData.results
      })

      this.currentCategory = this.urls[value].name
      this.index = 0
    },
    addNum() {
      this.questionNum++
    },
    resetNum() {
      this.questionNum = 1
    }
  },
  mounted: function() {
    this.pickCategory(0)
  }
  // mounted: function(pickedCategory) {
  //   fetch(pickedCategory, {
  //     method: 'get'
  //   })
  //   .then((response) => {
  //     return response.json()
  //   })
  //   .then((jsonData) => {
  //     this.questions = jsonData.results
  //   })
  // }
}
</script>

<style>
#app {
  font-family: Montserrat, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  min-height: 100vh;
  text-align: center;
  color: #f2f2f2;
  background: linear-gradient(120deg, rgba(1,85,140,1) 0%, rgba(4,112,141,1) 25%, rgba(4,139,126,1) 50%, rgba(9,166,123,1) 75%, rgba(5,191,125,1) 100%);
}
</style>
