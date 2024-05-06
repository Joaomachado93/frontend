<template>
  <div id="app">
    <TopBar @opinionArticlesClicked="scrollToOpinionArticles" />
    <SimpleCarousel />
    <CardsCarousel ref="cardsCarousel" :sliders="sliders" />
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
  },
  data() {
    return {
      sliders: [
        { imgUrl: require('@/assets/images-card.jpg'), title: "GI products such as figs, pepper and olive oil grow under cooperation between the EU and Africa", img: require('@/assets/person2.jpg'), name: "Inês Monteiro Alves", date: "12 julho 2023" },
        { imgUrl: require('@/assets/black.jpg'), title: "Influencers and Brand Defamation", img: require('@/assets/person1.jpg'), name: "Rute Franco", date: "12 julho 2023" },
        { imgUrl: require('@/assets/images-card.jpg'), title: "Innovations in Sustainable Architecture", img: require('@/assets/person3.jpg'), name: "Rute Franco", date: "12 julho 2023" }
      ]
    };
  },
  methods: {
// App.vue
scrollToOpinionArticles() {
  const carouselElement = this.$refs.cardsCarousel.$refs.sliderContainer;
  if (carouselElement) {
    carouselElement.scrollIntoView({ behavior: 'smooth' });
  }
}


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
