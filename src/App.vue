<template>
  <div id="app">
    <contact-form></contact-form>
    <div class="container">
      <img alt="Vue logo" src="./assets/logo.png">
      <br><br><br>
      <h1>Simple Contact Form</h1>
      <br>
      <h2>Vue.js CLI3, Bootstrap-vue.js, Bootstrap 4, SASS</h2>
      <br>
      <hr>
      <p>Press "Contact Me" button.</p>
    </div>
  </div>
</template>

<script>
import ContactForm from './components/ContactForm.vue'

export default {
  name: 'app',
  components: {
    ContactForm
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
