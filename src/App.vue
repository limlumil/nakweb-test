<template>
  <div id="app">
    <CompanySlider />
  </div>
</template>

<script>
import CompanySlider from './components/CompanySlider.vue'

export default {
  name: 'App',
  components: {
    CompanySlider
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
