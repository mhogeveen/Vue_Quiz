<template>
  <div class="header-container">
    <b-nav tabs>
      <b-nav-item disabled><b>QUIZIT</b></b-nav-item>
      <b-nav-item disabled>Counter: {{numCorrect}} / {{numTotal}}</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
  export default {
    props: [
      'numCorrect',
      'numTotal'
    ]
  }
</script>

<style lang="css" scoped>
  .nav-item a.disabled {
    color: #f2f2f2;
  }
  .nav {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .nav-item:first-child {
    font-size: 25px;
  }
  .header-container {
    background: rgba(255,255,255,0.2);
  }
</style>
