<template>
  <div class="main-container">
    <MainImage></MainImage>
    <FeedbackForm></FeedbackForm>
  </div>
</template>

<script>
import MainImage from './components/MainImage.vue'
import FeedbackForm from './components/FeedbackForm.vue'

export default {
  name: 'App',
  components: {
    MainImage,
    FeedbackForm
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  border: 1px solid red;
  background: #FFFFFF;
  width: 100%;
  height: auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
.main-container {
  border: 1px solid red;
  width: auto;
  max-width: 80%;
  height: 90vh;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  gap: 60px;
}

</style>
