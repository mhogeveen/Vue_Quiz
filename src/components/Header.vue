<template>
  <div>
    <b-nav tabs>
      <b-nav-item disabled><b>Fancy Quiz App</b></b-nav-item>
      <b-nav-item disabled>Counter: {{numCorrect}}/{{numTotal}}</b-nav-item>
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
    color: #0d0d0d;
  }

  .nav {
    display: flex;
    justify-content: center;
  }
</style>
