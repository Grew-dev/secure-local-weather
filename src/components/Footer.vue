<template>
  <footer>
    <small>Powered by <b><a href="https://pointng.io" target="_blank">pointNG</a></b></small>
    <small> <div>Icons made by <a href="https://www.flaticon.com/authors/fjstudio" title="fjstudio">fjstudio</a> and <a href="http://www.freepik.com/" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a></div></small>
       <small> <div><a href="https://github.com/Grew-dev/grew-privacy-policy" title="Privacy Policy">Privacy Policy</a></div></small>
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
