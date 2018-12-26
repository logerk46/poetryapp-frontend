<template>
    <div class="home">
        <div class="container">
            <div class="site-body col-md-12">
                <div class="row">
                    <div class="site-logo__wrapper col-md-6">
                        <img class="site-logo" src="../assets/logo.png">
                        <div @click="getAuthor()" class="start-button col-md-4 text-center mx-auto">
                            <span class="start-button_text">Let's find out</span>
                        </div>
                    </div>
                    <transition name="fade" mode="out-in">
                        <div v-if="!showAuthor" key="poem-form" class="site-title__wrapper col-md-6">
                            <h1>Want to know who are you from poets?</h1>
                            <h4>Write your piece of poetry in the form below</h4>
                            <div class="poetry-input__wrapper">
                                <textarea v-model="poem"
                                          cols="63" rows="20"
                                          placeholder="Do it!"></textarea>
                            </div>
                        </div>
                        <poet-info class="col-md-6"
                                   v-if="showAuthor"
                                   key="poet-info"
                                   :poetData="this.poetData"/>
                    </transition>
                </div>
            </div>
            <div class="footer text-center">
                <div class="author-about text-center">
                    <router-link to="/about"><h5>How it's work?</h5></router-link>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import PoetInfo from '../components/PoetInfo.vue';

export default {
  components: {
    PoetInfo,
    'poet-info': PoetInfo,
  },
  data() {
    return {
      poets: ['William_Shakespeare',
        'Katherine_Mansfield',
        'Malcolm_Cowley',
        'Conrad_Aiken',
        'Archibald_Macleish'],
      poem: '',
      poetData: null,
      showAuthor: false,
    };
  },
  methods: {
    getAuthor() {
      axios.get(`https://en.wikipedia.org/api/rest_v1/page/summary/${this.poets[Math.floor(Math.random() * this.poets.length)]}`)
        .then((response) => {
          this.poetData = response.data;
        });
      this.showAuthor = !this.showAuthor;
      this.poem = '';
    },
  },
};
</script>

<style>
    .fade-enter-active,
    .fade-leave-active {
        transition: opacity .5s;
    }

    .fade-enter,
    fade-leave-to {
        opacity: 0;
    }

    .site-body {
        margin-top: 125px;
    }

    .site-logo {
        width: 100%;
    }

    .site-title__wrapper h4 {
        color: rgba(0, 0, 0, 0.4);
    }

    .poetry-input__wrapper {
        margin-top: 20px;
    }

    .poetry-input__wrapper textarea {
        padding: 10px;
        max-width: 100%;
        resize: none;
    }

    .start-button {
        background-color: black;
        height: 60px;
        margin-top: 18%;
        cursor: pointer;
        padding-top: 16px;
        box-shadow: 0 0 11px rgba(33, 33, 33, .2);
    }

    .start-button_text {
        font-family: 'Roboto Condensed', sans-serif;
        font-size: 19px;
        color: white;
    }

    .start-button:hover {
        box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
    }

    .poetry-input__wrapper textarea:focus {
        outline: none;
        box-shadow: 0 0 11px rgba(33, 33, 33, .2);
    }
    .footer {
        position: fixed;
        left: 0;
        bottom: 0;
        width: 100%;
        height: 75px;
    }
    .author-about a{
        color: black;
        text-decoration: none;
    }
</style>
