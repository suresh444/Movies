<template>
  <div id="app">
    <movie-rating/>
  </div>
</template>

<script>
import movieRating from './components/movies.vue'

export default {
  name: 'App',
  components: {
      movieRating
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
