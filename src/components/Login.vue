<template>
  <div>
      <header class="header">
            <div class="header__logo">
              <router-link to="/"><h1 class="h1--logo">myLibrary</h1></router-link>
              <h2 class="h2--logo">Admin Login</h2>
          </div>
      </header>

      <main>
        <div class="main--container">
          <div class="section">
            <form class="form--login" @submit.prevent="login">
              <input class="form__el" v-model="email" type="text" id="inputEmail" placeholder="ID" required autofocus>
              <input class="form__el" v-model="password" type="password" id="inputPassword" placeholder="Password" required>
              <button class="form__sumbit" v-on:click="signIn">Login</button>
            </form>
          </div>
        </div>
      </main>

      <footer class="footer footer--bottom">
          <div class="footer--container">
            <h1 class="footer--title">
              © Adrian Orłów
            </h1>
          </div>
      </footer>
  </div>
</template>

<script>
import Firebase from 'firebase'

export default {
  name: 'Login',
  beforeCreate: function() {
      if (this.$parent.user != null) {
        this.$router.replace('panel')
      }
      Firebase.auth().onAuthStateChanged((user) => {
        if (user) {
          this.$parent.user = user
        }
      })
  },
  data: function () {
    return {
      email: '',
      password: '',
      user: null
    }
  },
  methods: {
    signIn: function() {
      Firebase.auth().signInWithEmailAndPassword(this.email, this.password).then(
        (user) => {
          this.$router.replace('panel')
        },
        (err) => {
          alert('Error: ' + err.message)
        }
      )
    }
  }
}
</script>
