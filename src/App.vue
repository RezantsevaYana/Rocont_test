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
body {
  margin: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  height: 100vh;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #FFFFFF;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.main-container {
  width: auto;
  max-width: 1047px;
  height: 95vh;
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  gap: 60px;

  @media screen and (max-width: 1024px) {
    gap: 0;
    height: 100%;
  }
}

</style>
