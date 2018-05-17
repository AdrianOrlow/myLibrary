<template>
  <div v-if="this.$parent.user">
      <header class="header">
            <div class="header__logo">
              <router-link to="/"><h1 class="h1--logo">myLibrary</h1></router-link>
              <h2 class="h2--logo">Admin Panel</h2>
          </div>
      </header>

      <main>
        <div class="main--container">
          <div class="section">
            <div class="table--container" v-if="noPopup">
              <input class="table__input" type='text' placeholder="Search" v-model="search">
              <table class="table">
                <thead>
                  <tr>
                    <th>Title</th>
                    <th>Author</th>
                    <th>Action</th>
                  </tr>
                </thead>
              
                <tbody>
                  <tr v-for="book in filteredBooks" v-bind:key="book.id">
                    <td>{{book.Title}}</td>
                    <td>{{book.Author}}</td>
                    <td>
                      <i class="icon fa-ellipsis-v"></i>
                      <div class="table__dropdown">
                        <a class="table__dropdown__el" v-on:click="moreClicked(book)">More</a>
                        <a class="table__dropdown__el" v-on:click="editClicked(book)">Edit</a>
                        <a class="table__dropdown__el" v-on:click="removeBook(book)">Delete</a>
                      </div>
                    </td>
                  </tr>
                </tbody>
              </table>
              <a class="table__button" v-on:click="addClicked()">Add</a>
            </div>
            <div class="popup popup--small" v-if="showMore">
                <div class="popup--container">
                  <h1 class="popup__title">More</h1>
                    <p class="popup__label">Title: </p>
                    <p class="form__el popup__el popup__el--center">{{editBook.Title}}</p>
                    <p class="popup__label">Author: </p>
                    <p class="form__el popup__el popup__el--center">{{editBook.Author}}</p>
                    <p class="popup__label">Imglink: </p>
                    <p class="form__el popup__el popup__el--center"><a :href="editBook.Imglink">Link</a></p>
                    <p class="popup__label">ISBN: </p>
                    <p class="form__el popup__el popup__el--center">{{editBook.Isbn}}</p>
                    <p class="popup__label">Status: </p>
                    <p class="form__el popup__el popup__el--center">{{editBook.Status}}</p>
                    <button class="form__cancel addbook__cancel" type="cancel" v-on:click="showMore = false; closePopup()">Close</button>
                </div>
            </div>
            <div class="popup" v-if="showEdit">
                <div class="popup--container">
                  <h1 class="popup__title">Edit book</h1>
                  <form class="popup__form" v-on:submit.prevent="updateBook">
                    <label for="inputTitle" class="popup__label">Title: </label>
                    <input class="form__el popup__el" v-model="editBook.Title" type="text" id="inputTitle" required autofocus>
                    <label for="inputAuthor" class="popup__label">Author: </label>
                    <input class="form__el popup__el" v-model="editBook.Author" type="text" id="inputAuthor" required>
                    <label for="inputImglink" class="popup__label">Imglink: </label>
                    <input class="form__el popup__el" v-model="editBook.Imglink" type="text" id="inputImglink" required>
                    <label for="inputIsbn" class="popup__label">ISBN: </label>
                    <input class="form__el popup__el" v-model="editBook.Isbn" type="text" id="inputIsbn" required>
                    <label for="inputStatus" class="popup__label">Status: </label>
                    <select class="form__el popup__el popup__select" v-model="editBook.Status" type="text" id="inputStatus" required>
                      <option value="Available">Available</option>
                      <option value="Unavailable">Unavailable</option>
                    </select>
                    <button class="form__cancel addbook__cancel" type="cancel" v-on:click="showEdit = false; closePopup()">Cancel</button>
                    <button class="form__sumbit addbook__sumbit" type="submit">Update</button>
                  </form>
                </div>
            </div>
            <div class="popup" v-if="showAddBook">
                <div class="popup--container">
                  <h1 class="popup__title">Add book</h1>
                  <form class="popup__form" v-on:submit.prevent="addBook">
                    <label for="inputTitle" class="popup__label">Title: </label>
                    <input class="form__el popup__el" v-model="newBook.Title" type="text" id="inputTitle" required autofocus>
                    <label for="inputAuthor" class="popup__label">Author: </label>
                    <input class="form__el popup__el" v-model="newBook.Author" type="text" id="inputAuthor" required>
                    <label for="inputImglink" class="popup__label">Imglink: </label>
                    <input class="form__el popup__el" v-model="newBook.Imglink" type="text" id="inputImglink" required>
                    <label for="inputIsbn" class="popup__label">ISBN: </label>
                    <input class="form__el popup__el" v-model="newBook.Isbn" type="text" id="inputIsbn" required>
                    <label for="inputStatus" class="popup__label">Status: </label>
                    <select class="form__el popup__el popup__select" v-model="newBook.Status" type="text" id="inputStatus" required>
                      <option value="Available">Available</option>
                      <option value="Unavailable">Unavailable</option>
                    </select>
                    <button class="form__cancel addbook__cancel" type="cancel" v-on:click="showAddBook = false; closePopup()">Cancel</button>
                    <button class="form__sumbit addbook__sumbit" type="submit">Add</button>
                  </form>
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
                  <p class="footer--link" v-on:click="logout">Log out</p>
                </ul>
            </div>
          </div>
      </footer>
  </div>
</template>

<script>

import Firebase from 'firebase'

export default {
  name: 'Panel',
  data () {
    return {
      noPopup: true,
      search: '',
      showAddBook: false,
      showMore: false,
      showEdit: false,
      book: '',
      Title: '',
      Author: '',
      Imglink: '',
      Isbn: '',
      Status: '',
      newBook: {
        Title: '',
        Author: '',
        Imglink: '',
        Isbn: '',
        Status: ''
      },
      editBook: {
        Title: '',
        Author: '',
        Imglink: '',
        Isbn: '',
        Status: ''
      }
    }
  },
  beforeCreate: function() {
      if (this.$parent.user == null) {
        this.$router.replace('login')
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
  },
  methods: {
    logout: function () {
      Firebase.auth().signOut().then(() => {
        this.$parent.user = null
        this.$router.replace('login')
      })
    },
    addClicked: function () {
        this.showAddBook = true;
        this.noPopup = false;
        document.documentElement.scrollTop = 0;
    },
    addBook: function () {
        booksRef.push(this.newBook);
        this.newBook.Title = '';
        this.newBook.Author = '';
        this.newBook.Imglink = '';
        this.newBook.Isbn = '';
        this.newBook.Status = '';
    },
    moreClicked: function(book) {
        	this.editBook.Title = book.Title;
          this.editBook.Author = book.Author;
          this.editBook.Imglink = book.Imglink;
          this.editBook.Isbn = book.Isbn;
          this.editBook.Status = book.Status;
					this.showMore = true;
          this.noPopup = false;
          document.documentElement.scrollTop = 0;
    },
    editClicked: function(book) {
          this.book = book;
        	this.editBook.Title = book.Title;
          this.editBook.Author = book.Author;
          this.editBook.Imglink = book.Imglink;
          this.editBook.Isbn = book.Isbn;
          this.editBook.Status = book.Status;
					this.showEdit = true;
          this.noPopup = false;
          document.documentElement.scrollTop = 0;
    },
    updateBook: function (book) {
        booksRef.child(this.book['.key']).update(this.editBook);
        this.showEdit = false;
        this.noPopup = true;
        this.editBook.Title = '';
        this.editBook.Author = '';
        this.editBook.Imglink = '';
        this.editBook.Isbn = '';
        this.editBook.Status = '';
    },
    removeBook: function (book) {
      booksRef.child(book['.key']).remove()
    },
    closePopup: function () {
      this.noPopup = true;
    }
  }
}
</script>
