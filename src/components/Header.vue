<template>
  <footer>
    <h1>Secure Local Weather</h1>
  </footer>
</template>

<script>
export default {
  name: 'Header',
}
</script>

<style scoped>
footer {
  text-align: center;
  position: absolute;
  top: 20px;
  visibility: hidden;
}

@media screen and (min-width: 450px) {
  footer {
    visibility: visible;
  }
}
</style>
