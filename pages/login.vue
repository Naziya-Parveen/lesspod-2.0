<template>
  <div>
    <Navbar :menus="menus"/>
    <div class="container">
      <br /><br><br>
      <h3>Let's Login</h3>
      <b-form v-if="show" @submit="onSubmit" @reset="onReset">
        <b-form-group
          id="emailInputGroup"
          label="Email address:"
          label-for="emailInput"
        >
          <b-form-input
            id="emailInput"
            v-model="form.email"
            type="text"
            required
            placeholder="Enter email"
          />
        </b-form-group>
        <b-form-group
          id="passwordInputGroup"
          label="Password:"
          label-for="passwordInput"
        >
          <b-form-input
            id="passwordInput"
            type="password"
            v-model="form.password"
            required
            placeholder="Enter password"
          />
        </b-form-group>
        <b-button type="submit" variant="primary">
          Login
        </b-button>
        <!-- <b-button type="reset" variant="danger">
            Reset
          </b-button> -->
      </b-form>
      <span style="margin-top: 0.7rem;">If you don't have an account, you can <a href="/signup">Create An Account</a>.</span>
    </div>
    <Footer />
  </div>
</template>

<style></style>

<script>
import Navbar from '../components/NavbarBS.vue'
import Footer from '../components/Footer.vue'
import contentProcessing from '~/mixins/contentProcessing.js'
export default {
  mixins: [contentProcessing],
  components: {
    Navbar,
    Footer
  },
  data() {
    return {
      form: {
        email: '',
        password: '',
        name: '',
        checked: []
      },
      show: true
    }
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault()
      // alert(JSON.stringify(this.form))
      this.$store.dispatch('login', {
          username: this.form.email,
          password: this.form.password
      });
      // this.$auth.loginWith('local', {
      //   data: {
      //     username: this.form.email,
      //     password: this.form.password
      //   }
      // })
    },
    onReset(evt) {
      evt.preventDefault()
      /* Reset our form values */
      this.form.email = ''
      this.form.name = ''
      this.form.checked = []
      /* Trick to reset/clear native browser form validation state */
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    }
  }
}
</script>
