<template>
  <div id="app">
    <TopBar />
    <SimpleCarousel />
   <CardsCarousel />
  </div>
</template>

<script>
import TopBar from './components/TopBar.vue'
import SimpleCarousel from './components/SimpleCarousel.vue'
import CardsCarousel from './components/CardsCarousel.vue'

export default {
  name: 'App',
  components: {
    TopBar,
    SimpleCarousel,
    CardsCarousel
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
}
</style>
