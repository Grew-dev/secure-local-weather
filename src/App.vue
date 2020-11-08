<template>
  <div id="app">
    <div class="secure-weather">
      <Header></Header>
      <SecureWeather></SecureWeather>
      <Footer></Footer>
    </div>
  </div>
</template>

<script>
import SecureWeather from './components/SecureWeather'
import Footer from './components/Footer'
import Header from './components/Header'

export default {
  name: 'App',

  components: {
    SecureWeather,
    Footer,
    Header
  }
}
</script>

<style>

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
  -webkit-font-smoothing: antialiased;
  color: rgba(255, 255, 255, 0.925);
}

a {
  text-decoration: none;
  color: inherit;
  transition: color .1s ease-in;
}

a:hover {
  color: rgba(46, 146, 167, 0.925);
}

.secure-weather {
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to bottom right, #1f364d, #1f364d) no-repeat;
}

</style>
