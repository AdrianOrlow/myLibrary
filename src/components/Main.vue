<template>
  <div>
    <header class="header">
          <div class="header__logo">
              <router-link to="/"><h1 class="h1--logo">myLibrary</h1></router-link>
          </div>
    </header>
    <main>
        <div class="main--container main--white">
          <div class="section section--search">
            <div class="search--container">
                <input v-model="search" class="search__input" type='text' placeholder="Search for books">
            </div>
          </div>
          <div class="section section--books" v-if="search">
            <div class="book" v-for="book in filteredBooks" v-bind:key="book.id">
              <div class="book--container">
                <div class="book__info">
                  <h1 class="book__title">{{book.Title}}</h1><br>
                  <h2 class="book__author">by {{book.Author}}</h2>
                  <img class="book__cover" :src="book.Imglink">
                  <h2 class="book__status">{{book.Status}}</h2>
                </div>
              </div>
            </div>
          </div>
        </div>
      </main>

      <footer class="footer footer--bottom">
          <div class="footer--container">
            <h1 class="footer--title">
              © Adrian Orłów
            </h1>

            <div class="footer--nav">
              <ul class="footer--list">
                <router-link to="/login"><p class="footer--link">Admin panel</p></router-link>
              </ul>
            </div>
          </div>
      </footer>
  </div>
</template>

<script>
import Firebase from 'firebase'
var config = {
  apiKey: "AIzaSyBKLjkwGlRkySMZqUgn9iRsfrbHgjL8W2Y", 
  authDomain: "mylibrary-ato.firebaseapp.com", 
  databaseURL: "https://mylibrary-ato.firebaseio.com", 
  projectId: "mylibrary-ato", 
  storageBucket: "", 
  messagingSenderId: "846912325877"
};
  
let app = Firebase.initializeApp(config);
let db = app.database()
window.booksRef = db.ref('books')

export default {
  name: 'Main',
  data: function () {
    return {
      search: ''
    }
  },
  firebase: {
    books: booksRef
  },
  computed: {
    filteredBooks() {
      return this.books.filter(book => {
         return book.Title.toLowerCase().indexOf(this.search.toLowerCase()) !== -1
      })
    }
  }
}
</script>
