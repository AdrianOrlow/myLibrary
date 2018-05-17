<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      user: null
    }
  }
}
</script>

<style>
/* Reset */

html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, embed, figure, figcaption, footer, header, hgroup, menu, nav, output, ruby, section, summary, time, mark, audio, video {
    margin: 0;
    padding: 0;
    border: 0;
    font-size: 100%;
    font: inherit;
    vertical-align: baseline;
}

article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section {
    display: block;
}

body {
    line-height: 1;
}

ol, ul {
    list-style: none;
}

blockquote, q {
    quotes: none;
}

blockquote:before, blockquote:after, q:before, q:after {
    content: '';
    content: none;
}

table {
    border-collapse: collapse;
    border-spacing: 0;
}

body {
    -webkit-text-size-adjust: none;
}   

textarea,input {
    border: none;
    overflow: auto;
    outline: none;
    resize: none;
    -webkit-box-shadow: none;
    -moz-box-shadow: none;
    box-shadow: none;
}

*:focus {
    outline: none;
}

/* Basic */

body {
    font-family: 'Montserrat', sans-serif;
}

a {
    text-decoration: none;
    color: #333;
}

    a:visited {
        color: #333;
    }

.hidden {
    display: none;
}

/* Icon */

.icon {
    text-decoration: none;
    position: relative;
}

    .icon:before {
        font-family: FontAwesome;
        font-style: normal;
        font-weight: normal;
        text-transform: none !important;
    }

/* Header */

.header {
    font-family: "Montserrat", sans-serif;
    font-weight: 600;
    width: 100%;
}

    .header__logo {
        margin: 3.3em 0 6.6em;
        display: block;
        text-align: center;
        align-items: center;
        justify-content: center;
    }

    .h1--logo {
        cursor: pointer;
        font-size: 3.5em;
        width: auto;
        font-weight: 700;
    }

    .h2--logo {
        font-size: 1.5em;
        margin-top: 0.5em;
    }

@media (max-width: 43em) {
    .h1--logo {
        float: none;
        text-align: center;
        font-size: 3em;
    }
}

/* Main */

    .main--container {
        width: 80%;  
        margin: 40px auto 6em;
    }

    .main--white {
        background: #ffff;
    }

/* Sections */

    .section {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .section--search {
        margin-bottom: 6.6em;
    }

    .section--books {
        display: grid;
        grid-gap: 2em;
        grid-template-columns: auto auto auto auto;
    }

/* Search */

    .search__input {
        background-color: #f5f5f5;
        border: none;
        border-radius: 0.3em;
        font-size: 2.5em;
        line-height: 1.25em;
        padding: 0.5em 1em;
        transition: ease-in-out 0.2s;
        width: 15em;
   }

        .search__input:focus {
           background-color: #ececec; 
        }

        .search__input:focus::-webkit-input-placeholder {
            opacity: 0;
        }
/* Books */

    .book {
        height: 23.04em;
        width: 14.4em;
        background: #f5f5f5;
        border-radius: 0.5em;
        position: relative;
        margin-left: 1em;
    }

    .book--container {
        padding: 2em 1em;
    }

    .book__title {
        font-size: 1.4em;
        font-weight: 700;
        text-align: center;
    }

    .book__author {
        font-size: 1.1em;
        font-weight: 600;
        font-style: italic;
        line-height: 0em;
        color: #333;
    }

    .book__status {
        position: absolute;
        bottom: 2em;
        right: 0;
        left: 0;
    }

    .book_author, .book__title, .book__author, .book__status {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .book__cover {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateX(-50%) translateY(-40%);
        width: 7em;
        height: auto;
    }

/* Login Form */

        .form__el {
            display: block;
            background-color: #f5f5f5;
            border: none;
            border-radius: 0.3em;
            font-size: 1.25em;
            line-height: 1.25em;
            padding: 0.5em 1em;
            transition: ease-in-out 0.2s;
            width: 8em;
            margin-bottom: 1em;
        }

            .form__el:focus {
            background-color: #ececec; 
            }

            .form__el:focus::-webkit-input-placeholder {
                opacity: 0;
            }

        .form__sumbit, .form__cancel {
            background-color: #f5f5f5;
            border: none;
            border-radius: 0.3em;
            font-size: 1.25em;
            line-height: 1.25em;
            padding: 0.5em 1em;
            transition: ease-in-out 0.2s;
            width: 5em;
            float: right;
            margin-bottom: 1em;
            font-weight: 600;
            cursor: pointer;
        }

            .form__sumbit:hover, .form__cancel:hover {
                background-color: #ececec; 
            }

            .form__sumbit:active, .form__cancel:active {
                background-color: #bcbcbc; 
            }

        .form__cancel {
            float: left;
        }

/* Admin Panel Table */

    .table__input {
        background-color: #f5f5f5;
        font-size: auto;
        line-height: 1.25em;
        padding: 0.5em 1em;
        transition: ease-in-out 0.1s;
        width: 34em;
    }

        .table__input:focus {
        background-color: #ececec; 
        }

        .table__input:focus::-webkit-input-placeholder {
            opacity: 0;
        }

    .table__button {
        display: block;
        background-color: #f5f5f5;
        font-size: auto;
        line-height: 1.25em;
        padding: 1em;
        transition: ease-in-out 0.1s;
        width: 28em;
        height: 1em;
        text-align: center;
        cursor: pointer;
    }

        .table__button:hover {
        background-color: #ececec; 
        }

        .table__button:active {
            background-color: #bcbcbc; 
        }

    table {
        border-collapse: collapse;
        width: 30em;
    }
    th {
        background: #ececec;
    }
    
    th, td {
        border: 1px solid #ececec;
        padding: 1em;
        text-align: center;
    }

    tr {
        transition: ease-in-out 0.2s;
        background: #fff;
    }
    
    tr:nth-child(even) {
        background: #fafafa;
    }

    td:nth-child(3) {
        background: #f3f3f3;
        width: 10%;
        font-weight: 600;
        transition: ease-in-out 0.2s;
    }

        td:nth-child(3):hover {
            background: #f1f1f1;
            cursor: pointer;
        }

        td:nth-child(3):active {
            background: #bcbcbc;
            cursor: pointer;
        }
    
    tr:hover {
        background: #f5f5f5;
    }


/* Admin Panel Table Dropdown Menu */

    .table__dropdown {
        display: none;
        position: absolute;
        background-color: #f3f3f3;
        width: 8em;
        z-index: 1;
        margin: 1em 0 0 -1em;
    }

        .table__dropdown__el {
            color: black;
            padding: 1em 1.5em;
            text-decoration: none;
            display: block;
        }

        .table__dropdown__el:hover {
            background-color: #ececec;
        }

        .table__dropdown__el:active {
            background-color: #bcbcbc;
        }

    td:nth-child(3):hover .table__dropdown {
        display: block;
    }

/* Admin Panel popup */

    .popup {
        background: #f5f5f5;
        width: 28em;
        height: auto;
        position: absolute;
        top: 14.6em;
        padding: 2em;
    }

    .popup--small {
        height: auto;
    }

    .popup--container {
        padding: 0 1.2em;
    }

    .popup__title {
        font-size: 1.5em;
        font-weight: 600;
        display: flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 1.2em;
    }

    .popup__el {
        display: block;
        margin-right: 0;
        margin-left: auto;
        border-radius: 0;
        border-bottom: #333;
        border-bottom-style: solid;
        width: 11.2em;
    }

        .popup__el--center {
            text-align: center;
        }

        .popup__select {
            width: 13.2em;
        }

select option:checked:after {
    content: attr(title);
    background: #666;
    color: #fff;
    position: absolute;
    width: 100%;
    left: 0;
    border: none;
}
    .popup__label {
        float: left;
        line-height: 2.75em;
        font-size: 1.25em;
        font-weight: 600;
        margin-left: 0;
    }

    .addbook__sumbit, .addbook__cancel {
        margin-top: 1.2em;
        width: 5.2em;
        text-align: center;
    }

    .addbook__sumbit {
        border-radius: 0em;
        background: #333;
        color: #fafafa;
        margin-right: 0;
    }

        .addbook__sumbit:hover {
            background-color: #444; 
        }

        .addbook__sumbit:active {
            background-color: #222; 
        }

    .addbook__cancel {
        border-radius: 0;
        margin-left: 0;
        background: #ececec;
    }

        .addbook__cancel:hover {
            background-color: #bcbcbc; 
        }

        .addbook__cancel:active {
            background-color: #adadad; 
        }

/* Footer */

    .footer {
        position: absolute;
        color: #333;
        width: 100%;
        height: 10vh;
        font-size: 1.2em;
        bottom: 0;
        z-index: -10;
    }

        .footer--bottom {
            position: fixed;
        }

        .footer--container {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin: 0 auto;
            padding: 0;
            height: 100%;
            width: 100%;
            max-width: 1200px;
        }

        .footer--title {
            font-weight: 600;
            font-family: "Montserrat";
        }
        
        .footer--link {
            text-transform: uppercase;
            font-weight: 600;
            cursor: pointer;
            padding: 0.7em;
            color: #fafafa;
            background: #333;
            font-size: 0.8em;
            border-radius: 1em;
            transition: ease-in-out 0.2s;
        }

        .footer--link:hover {
            background: #444;
        }
        
        .footer--link:active {
            background: #222;
        }



        /* Mobile */

        @media only screen and (max-width: 768px) {
            .main--container {
                width: 100%;
                margin: 40px auto 6em;
            }

            .section--search {
                position: sticky;
                top: 1em;
                z-index: 10;
            }

            .section--search:sticky {
                background: #333;
            }

            .search__input {
                width: 70vw;
                font-size: 2em;
            }

            .table__input {
                padding: 1em 4vw;
                width: 92vw;
                position: sticky;
                top: 0;
                z-index: 20;
            }

            .table {
                width: 100vw;
                z-index: 10;
            }

            .table__button {
                width: 92vw;
                padding: 4vw;
            }

            .table__dropdown {
                margin: 1em 0 0 0em;
                right: 0;
            }

            .popup {
                width: 100vw;
                padding: 2em 0;
            }

            .footer {
                width: 80vw;
                padding: 0 10vw;
            }
        }

        

        @media only screen and (max-width: 1100px) {
            .section--books {
                grid-template-columns: auto auto;
            }
        }

         @media only screen and (min-width: 767px) and (max-width: 1300px) {
            .footer {
                width: 80vw;
                padding: 0 10vw;
            }
         }

        @media only screen and (max-width: 500px) {
            .section--books {
                grid-template-columns: auto;
            }
        }

        
</style>
