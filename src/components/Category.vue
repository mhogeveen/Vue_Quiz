<template>
  <div>
    <div class="category-bar-container">
      <p class="catText">Choose a category:</p>
      <b-nav tabs align="center">
        <b-nav-item
          v-for="(url, index) in urls"
          :key="index"
          @click="pickCategory(index); resetNum()"
        >
          {{ url.name }}
        </b-nav-item>
      </b-nav>
    </div>
    <h4 class="currentCategory">Current category: {{ currentCategory }}</h4>
  </div>
</template>

<script>
  export default {
    props: {
      urls: Array,
      pickCategory: Function,
      resetNum: Function,
      currentCategory: String,
      questions: Array
    }
  }
</script>

<style lang="css" scoped>
  .nav-item a {
    color: #f2f2f2;
  }
  /* .nav {
    display: flex;
    justify-content: center;
  } */
  .catText {
    padding: 0.5rem 0 0 0;
    margin: 0;
    font-size: 1.25rem;
  }
  .currentCategory {
    margin: 2rem 0 0 0;
  }
  .category-bar-container {
    background: rgba(255,255,255,0.1);
  }
</style>
