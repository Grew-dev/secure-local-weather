<template>
  <footer>
    <small>Powered by <b><a href="https://pointng.io" target="_blank">pointNG</a></b></small>
  </footer>
</template>

<script>
export default {
  name: 'Footer',
}
</script>

<style scoped>
footer {
  text-align: center;
  position: absolute;
  bottom: 20px;
  visibility: hidden;
}

@media screen and (min-width: 450px) {
  footer {
    visibility: visible;
  }
}
</style>
