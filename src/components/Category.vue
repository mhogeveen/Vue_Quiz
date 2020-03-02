<template>
  <div>
    <p class="catText">Choose a category:</p>
    <b-nav tabs>
      <b-nav-item
        v-for="(url, index) in urls"
        :key="index"
        @click="pickCategory(index); resetNum()"
      >
        {{ url.name }}
      </b-nav-item>
    </b-nav>
  </div>
</template>

<script>
  export default {
    props: {
      urls: Array,
      pickCategory: Function,
      resetNum: Function
    }
  }
</script>

<style lang="css" scoped>
  .nav-item a.disabled {
    color: #0d0d0d;
  }
  .nav {
    display: flex;
    justify-content: center;
  }
  .catText {
    margin: 0.5rem 0 0 0;
    font-size: 1rem;
  }
</style>
