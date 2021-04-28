<template>
    <div v-if="!pending">
        <div class="kidsanna">
            <div class="container">
                <div class="kidsanna__wrapper">
                    <VueSlickCarousel class="carusel__sneakers" v-bind="settings">
                        <div class="carusel__sneakers-item" v-for="sneakers in colorData.sneakers" :key="sneakers.id" :id="sneakers.id">
                            <img class="carusel__sneakers--logo" :src="sneakers.img" alt="">
                        </div>
                    </VueSlickCarousel>
                    <div class="presence">
                        <div class="presence__head">
                            <div class="presence__head-instock" :class="colorData.presenceAvailable.class">{{colorData.presenceAvailable.title}}</div>
                            <div class="presence__head-vendorcode">{{colorData.presenceVendorCode}}</div>
                        </div>
                        <div class="presence__price">
                            <p class="presence__price-text--strike"><strike>{{colorData.priceProduct.value}}</strike><sub>{{colorData.priceProduct.productСurrency}}</sub></p>
                            <p class="presence__price-text">{{colorData.productPriceDiscount.value}}<sub>{{colorData.productPriceDiscount.productСurrency}}</sub></p>
                        </div>
                        <div class="presence__offer">
                            <h3 class="presence__offer-title">Цвет:</h3>
                            <label v-for="colors in viewsColor" :key="colors.id">
                                <input
                                :class="colors.class"
                                type="radio"
                                :id="colors.id"
                                name="age"
                                v-model="selectedСolor"
                                :value="colors.value"
                                />
                                <span :class="colors.class" class="colors"></span>
                            </label>
                        </div>
                        <button :class="colorData.kidsannaColorClass" class="kidsanna__product-buy">Купить</button>
                    </div>
                </div>
            </div>
        </div>
        <div v-if="pending">ПРЕЛОАДЕР</div>
    </div>
</template>

<script>
import VueSlickCarousel from 'vue-slick-carousel'
import 'vue-slick-carousel/dist/vue-slick-carousel.css'
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css'

export default {
  name: "kidsanna",
  components: { VueSlickCarousel },
  data: function () {
    return {  
        settings: {
            arrows: true,
        },
        pending: "true",
        selectedСolor: "ColorRed",   
        viewsColor: [
            {
            id: 1,
            value: "ColorRed",
            class: "presence__colors-red presence__colors"
            },
            {
            id: 2,
            value: "ColorGreen",
            class: "presence__colors-green presence__colors"
            },
            {
            id: 3,
            value: "ColorOrange",
            class: "presence__colors-orange presence__colors"
            },
        ],
        colorData: {},
    };
  },
  watch: {
    selectedСolor: {
      handler: function (val) {
        if (val == 'ColorRed') {
            console.log(val)
            this.axios.get("./static/color1.json").then((response) => {
            this.colorData = response.data;
            this.pending = false;
            console.log(this.colorData);
            });
        } else if (val == 'ColorGreen') {
            console.log(val)
            this.axios.get("./static/color2.json").then((response) => {
            this.colorData = response.data;
            this.pending = false;
            console.log(this.colorData);
            });
        } else if (val == 'ColorOrange') {
            console.log(val)
            this.axios.get("./static/color3.json").then((response) => {
            this.colorData = response.data;
            this.pending = false;
            console.log(this.colorData);
            });
        }
      },
      deep: true,
    },
  },
  created: function () {
    this.axios.get("./static/color1.json").then((response) => {
      this.colorData = response.data;
      this.pending = false;
      console.log(this.colorData);
    });
  },
};
</script>

<style scoped lang='scss'>
body {
    background: #F5F5F5;
}
input[type="radio"] {
    display: none;
    
}
.presence__colors {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    display: inline-block;
    box-sizing: border-box;
    position: relative;
    margin-left: 5px;
    cursor: pointer;
    &:checked + &,
    &:checked + &,
    &:checked + & {
        width: 30px;
        height: 30px;
        border: 2px solid #aaaaaa;
    }
    &-red {
        background-color: red;
    }
    &-green {
        background-color: green;
    }
    &-orange {
        background-color: orange;
    }
    &::before {
        content: '';
        background-image: url('../../src/assets/images/check/check.svg');
        width: 12px;
        height: 12px;
        right: -2px;
        top: -2px;
        position: absolute;
        opacity: 0;
        transition: all .2s;
    }
    &-red:checked + &::before,
    &-green:checked + &::before,
    &-orange:checked + &::before {
        opacity: 1;
    }
}

.presence__offer {
    display: block;
    text-align: left;
    &-title {
        font-weight: 500;
        font-size: 14px;
        line-height: 120%;
        color: #4F4F4F;
    }
}
.kidsanna {
    max-width: 1260px;
    margin: 0 auto;
    &__wrapper {
        display: flex;
    }
    &__product-buy {
        display: block;
        width: 210px;
        height: 50px;
        margin: 20px auto 0;
        border: none;
        border-radius: 30px;
        font-weight: bold;
        font-size: 14px;
        line-height: 100%;
        text-transform: uppercase;
        color: #FFFFFF;
        transition: all .2s;
        cursor: pointer;
    }

    &__color-red {
        background: red;
        border: 1px solid transparent;
        position: relative;
        padding-left: 20px;
        &::before {
            content: '';
            position: absolute;
            background-image: url('../../src/assets/images/basket.svg');
            width: 16px;
            height: 16px;
            left: 60px;
            top: 14px;
        }
        &:hover::before {
            background-image: url('../../src/assets/images/basket-red.svg');
        }
        &:hover {
            background-color: #fff;
            border: 1px solid red;
            color: red;
        }
    }

    &__color-green {
        background: green;
        border: 1px solid transparent;
        position: relative;
        padding-left: 20px;
        &::before {
            content: '';
            position: absolute;
            background-image: url('../../src/assets/images/basket.svg');
            width: 16px;
            height: 16px;
            left: 60px;
            top: 14px;
        }
        &:hover::before {
            background-image: url('../../src/assets/images/basket-green.svg');
        }
        &:hover {
            background-color: #fff;
            border: 1px solid green;
            color: green;
        }
    }

    &__color-orange {
        background: orange;
        border: 1px solid transparent;
        position: relative;
        padding-left: 20px;
        &::before {
            content: '';
            position: absolute;
            background-image: url('../../src/assets/images/basket.svg');
            width: 16px;
            height: 16px;
            left: 60px;
            top: 14px;
        }
        &:hover::before {
            background-image: url('../../src/assets/images/basket-orange.svg');
        }
        &:hover {
            background-color: #fff;
            border: 1px solid orange;
            color: orange;
        }
    }
}

.container {
    max-width: 1260px;
    margin: 0 auto;
}

.carusel__sneakers {
    width: 504px;
    height: 482px;
    margin-right: 20px;
    &-item {
        width: 504px;
        height: 482px;
    }
    &--logo {
        object-fit: cover;
        height: 500px;
    }
}
.presence {
    width: 50%;
    &__head {
    display: flex;
    justify-content: space-between;
    align-items: center; 
    width: 100%;
    }
    &__head-instock {
        padding: 5px 15px;
        font-weight: normal;
        font-size: 14px;
        line-height: 120%;
        border: 1px solid #969595;
        box-sizing: border-box;
        border-radius: 20px;
        display: flex;
        justify-content: center;
        align-items: center;      
    } 
    &__head--available {
        color: #00930F;
    }
    &__head--not-available {
        color: #930500;
    }
    &__head-vendorcode {
        font-size: 14px;
        line-height: 120%;
        color: #595959;     
    } 
    &__price {
        font-weight: bold;
        font-size: 30px;
        line-height: 100%;
        text-transform: uppercase;
        display: flex;
        justify-content: center;
        
    }
    &__price-text {    
        color: #F04137;
        sub {
            font-size: 12px;
        }
            &--strike {
            color: #828282;
            margin-right: 20px;
            sub {
                font-size: 12px;
            }
        }
    }
    &__colors-red,
    &__colors-green,
    &__colors-orange {
        width: 30px;
        height: 30px;
    }
}

.slick-prev:before,
.slick-next:before {
  font-family: 'slick';
  font-size: 20px;
  line-height: 1;

  opacity: 0.75;
  color: rgb(0, 0, 0) !important;

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

</style>
