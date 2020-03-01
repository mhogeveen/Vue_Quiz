<template>
  <div>
    <p class="catText">Choose a category:</p>
    <b-nav tabs>
      <b-nav-item >Animals</b-nav-item>
      <b-nav-item disabled>Mythology</b-nav-item>
      <b-nav-item disabled>Art</b-nav-item>
      <b-nav-item disabled>Sports</b-nav-item>
      <b-nav-item disabled>Science & Nature</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
  export default {

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
