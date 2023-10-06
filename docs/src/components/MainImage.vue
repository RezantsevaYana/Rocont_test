<template>
  <img
    src="../assets/main-image.png"
    alt="фоновая картинка"
    class="main-iamge"
  />
</template>

<script>
export default {
  name: "MainImage",
};
</script>

<style scoped lang="scss">
.main-iamge {
  flex-grow: 1;
  height: 100%;
  width: 52%;
  max-width: 550px;
  object-fit: cover;

  @media screen and (max-width: 600px) {
    display: none;
  }
}
</style>
