<template>
  <img src="../assets/main-image.png" alt="фоновая картинка" class="main-iamge">
</template>

<script>
export default {
  name: 'MainImage',
}
</script>

<style lang="scss">
.main-iamge {
  flex-grow: 1;
  height: 100%;
  object-fit: cover;
}

</style>
