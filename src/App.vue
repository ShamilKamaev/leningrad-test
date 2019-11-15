<template>
  <div id="app">
    <div class="open-form-block">
      <button 
        class="btn"
        @click="toggleShowForm">Click me to open form</button>
    </div>

    <transition name="fade" v-on:enter="enterForm">
      <app-form v-show="showForm" @hideForm="toggleShowForm"></app-form>
    </transition>
  </div>  
</template>

<script>
import anime from 'animejs/lib/anime.es.js';
import AppForm from './components/Form'

export default {
  components: {
    AppForm
  },

  data() {
    return {
      showForm: false
    }
  },

  methods: {
    toggleShowForm() {
      this.showForm = !this.showForm;
    },

    animateHeaderIn() {
      anime({
        targets: '.form__header span',
        opacity: 1,
        direction: 'forwards',
        delay: function(el, i, l) {
          return i * 50;
        }
      });
    },

    enterForm(el) {
      this.animateHeaderIn();
    },
  }
}
</script>

<style lang="scss">
// font-family: 'Big Shoulders Text', cursive;
// font-family: 'Raleway', sans-serif;
  body {
    margin: 0;
    padding: 0;
    color: #61bfad;
    font-family: 'Raleway', sans-serif; 
    * {
      box-sizing: border-box;
    }
  }

  .container {
    max-width: 1200px;
    margin: auto;
  }

  .open-form-block {
    min-height: 100vh;
    min-width: 100vw;
    background-color: #f9f7e8;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .btn {
    border: 1px solid #61bfad;
    padding: 8px 40px;
    border-radius: 99999px;
    color: #61bfad;
    background: transparent;
    font-family: 'Raleway', sans-serif; 
    font-size: 18px;
    font-weight: 100;
    outline: none;
    cursor: pointer;
    transition: transform .8s ease-out;
    text-align: center;
    &--send {
      color: #f9f7e8;
      border-color: #f9f7e8;
      width: 100%;
    }

    &:hover {
      @media (min-width: 1025px) {
        transform: scale(1.03);
      }
    }
    &:active {
      @media (min-width: 1025px) {
        // transition: transform 0s;
        transform: scale(1);
      }
    }
  }


  .fade-enter-active, .fade-leave-active {
    transition: opacity 600ms ease-in-out;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }
</style>
