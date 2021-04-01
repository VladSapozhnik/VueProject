<template>
  <div>
    
        <div class="popup__trigger" @click="openPopup">Open Popup</div>
        <transition name="popup">
          <div class="popup__wrapper" v-if="popupShow">
              <div class="popup__title">
                  <slot name='title'></slot>
              </div>
                  <div class="popup__close" @click="closePopup">X</div>
                  <transition name="counter-animation">
                    <button class="popup__btn-counter" @click="count++">Нажать</button>
                  </transition>
                  <div class="popup__number-click">{{ count }}</div> 
      
                <div @click='showResult = !showResult'>Показать результаты</div>
              <transition name="result-animation">
                <div class="popup__result" v-if="showResult">
                  <slot name='result'></slot>         
                </div> 
              </transition>
          </div>
        </transition>
        <transition name="popup-animation">
          <div class="shadow" v-on:click="closePopup" v-if="popupShow"></div>
        </transition>

  </div>
</template>

<script>
export default {
  name: 'popup',

  data: function() {
      return {
          count: 0,
          popupShow: false,
          showResult: false,
      }
  },
  methods: {
      openPopup: function () {
          this.popupShow = true
      },
      closePopup: function () {
          this.popupShow = false
      }
  },
}
</script>

<style scoped lang='scss'>

.popup-enter-active, .popup-leave-active {
  transition: opacity .2s;
}
.popup-enter, .popup-leave-to{
  opacity: 0;
}


.result-animation-enter {
  transform: translateX(150px);
  opacity: 0;
}

.result-animation-enter-active {
  transition: all 0.3s;
}

.result-animation-enter-to {
  opacity: 1;
  transform: rotateZ(5deg);
}

.result-animation-leave {
  opacity: 1;
}

.result-animation-leave-active {
  transition: all 0.3s;
}

.result-animation-leave-to {
  opacity: 0;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.popup__wrapper {
    max-width: 400px;
    width: 100%;
    min-height: 200px;
    border: 1px solid #000;
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 5;
    background-color: #fff;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    padding: 5px 25px;
}

.popup__btn-counter {
    width: 200px;
    height: 50px;
    background-color: rgb(61, 163, 170); 
    border: none;
    border-radius: 10px;
    color: #fff;
    outline: none;
}

.shadow {
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0, .6);
    position: fixed;
    left: 0;
    top: 0;
    z-index: 4;
}

.popup__trigger {
    border:1px solid #000;
    width: 100px;
    height: 50px;
    display: flex;
    width: 200px;
    height: 50px;
    background-color: rgb(61, 163, 170); 
    border: none;
    border-radius: 10px;
    color: #fff;
    justify-content: center;
    align-items: center;
    margin: 0 auto;
    cursor: pointer;
    outline: none; 
}

.popup__close {
    width: 10px;
    height: 10px;
    margin-left: auto;
    cursor: pointer;
}

</style>
