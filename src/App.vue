<template>
  <div id="app">
    <div class="container">
      <div class="text-center my-5">
        <img alt="Vue logo" src="./assets/logo.png" />
      </div>
      <form class="row g-3" @submit.prevent="handleSubmit">
        <div class="mb-3">
          <label for="exampleFormControlInput1" class="form-label">Email address</label>
          <input type="email" class="form-control" id="exampleFormControlInput1" placeholder="name@example.com">
        </div>
        <div class="mb-3">
          <label for="exampleFormControlTextarea1" class="form-label">Comment</label>
          <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"></textarea>
        </div>
        <vue-recaptcha ref="recaptcha" :sitekey="APP_SITE_SECRET" @verify="verifyMethod" @expired="expiredMethod"
          @render="renderMethod" @error="errorMethod" />
        <div class="col-auto">
          <button type="submit" class="btn btn-primary mb-3" :disabled="!disabled">Confirm identity</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { VueRecaptcha } from 'vue-recaptcha';

export default {
  name: 'App',
  data() {
    return {
      disabled: false,
      APP_SITE_SECRET: ''
    }
  },
  methods: {
    handleSubmit() {
      console.log('send request GET/POST')
    },
    verifyMethod() {

      this.disabled = true
    },
    expiredMethod() {
      console.log('expiredMethod')
    },
    renderMethod() {
      console.log('renderMethod')
    },
    errorMethod() {
      console.log('errorMethod')
    },

  },
  components: {
    VueRecaptcha
  },
  created() {
    this.APP_SITE_SECRET = process.env.VUE_APP_RECAPTCHAV2_SITEKEY
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
