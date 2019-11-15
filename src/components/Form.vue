<template>
  <div class="form__container">
    <button class="form__close-btn" @click="closeForm"> &#10005 </button>
    <div class="container">
      <form class="form" action="">
        <h2 class="form__header" ref="formHeader">Leningrad agency test</h2>
        <div class="input-group">
          <input 
            placeholder="email@adress"
            class="text-input" 
            type="text">
        </div>
        <div class="input-group">
          <input 
            placeholder="password"
            class="text-input" 
            type="password">
        </div>
        <div class="input-group input-group--checkbox">
          <input class="input-checkbox" type="checkbox" name="remeber-me" id="remember">
          <label for="remember" class="input-label"><span></span> remeber me</label>
        </div>
        <div class="input-group">
          <button class="btn btn--send" type="button">Send</button>
        </div>
      </form>
    </div>

  </div>
</template>

<script>
import anime from 'animejs/lib/anime.es.js';

export default {
  methods: {
    headerToArray() {
      let header = this.$refs.formHeader;
      let headerStr = header.textContent;
      let headerArr = headerStr.split('');
      let newHtml = '';
      headerArr.forEach(item => {
        newHtml += `<span style="opacity: 0; transform: translateY(10px)">${item}</span>`
      });
      header.innerHTML = newHtml;
    },


    closeForm() {
      anime({
        targets: '.form__header span',
        opacity: 0,
        direction: 'forwards',
        delay: function(el, i, l) {
          return i * 40;
        },
        begin: anim => {
          setTimeout(() => {
            this.$emit('hideForm');
          }, 300)
        }
      });
      
    }
  },


  mounted() {
    this.headerToArray();
  }
}
</script>

<style lang="scss">
  .form__container {
    position: absolute;
    left: 0;
    top: 0;
    width: 100vw;
    height: 100vh;
    background-color: #61bfad;
    padding-left: 15px;
    padding-right: 15px;
  }

  .form {
    width: 100%;
    padding-top: 48px;
    padding-bottom: 48px;
    display: flex;
    flex-wrap: wrap;
  }

  .form__close-btn {
    outline: none;
    width: 39px;
    height: 39px;
    padding: 0;
    position: absolute;
    right: 8px;
    top: 8px;
    color: #f9f7e8;
    border: 1px solid #f9f7e8;
    background: transparent;
    border-radius: 50%;
  }

  .form__header {
    color: #f9f7e8;
    font-family: 'Big Shoulders Text', cursive;
    text-transform: uppercase;
    letter-spacing: 4px;
    padding-left: 8px;
    padding-right: 8px;
    margin-bottom: 48px;
    margin-top: 0px;
    width: 100%;
  }

  .input-group {
    margin-bottom: 48px;
    width: 100%;
    &:nth-child(odd) {
      @media (min-width: 765px) {
        padding-left: 8px;
      }
    }
    &:nth-child(even) {
      @media (min-width: 765px) {
        padding-right: 8px;
      }
    }
    @media (min-width: 765px) {
      width: 50%; 
    }
  }


  .input-checkbox {
    display: none;
  }

  .input-checkbox:checked + .input-label {
    span {
      &::before {
        transform: translateX(calc(100% + 4px));
        background-color: #f9f7e8;
      }
    }
  }


  .input-label {
    color: #f9f7e8;
      display: flex;
      align-items: center;
      align-content: center;
      font-size: 18px;
    span {
      display: inline-block;
      width: 80px;
      height: 39px;
      border: 1px solid #f9f7e8;
      border-radius: 9999px;
      position: relative;
      margin-right: 16px;
      &::before {
        box-sizing: border-box;
        content: '';
        width: calc(50% - 4px);
        height: calc(100% - 4px);
        position: absolute;
        display: inline-block;
        top: 2px;
        left: 2px;
        background-color: transparent;
        border: 1px solid #f9f7e8;
        border-radius: 9999px;
        transition: transform .8s ease, background-color ease .8s;
      }
    }
  }





  .text-input {
    width: 100%;
    outline: none;
    background-color: transparent;
    border: none;
    border-bottom: 1px solid #f9f7e8;
    font-size: 18px;
    padding-left: 8px;
    padding-right: 8px;
    padding-bottom: 8px;
    color: #f9f7e8;
    font-family: 'Raleway', sans-serif;
    letter-spacing: 6px;
    &::-webkit-input-placeholder { /* Edge */
      color: rgba(249, 247, 232, 0.7);
    }

    &:-ms-input-placeholder { /* Internet Explorer 10-11 */
      color: rgba(249, 247, 232, 0.7);
    }

    &::placeholder {
      color: rgba(249, 247, 232, 0.7);
    }
  }
</style>