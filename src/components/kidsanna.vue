<template>
    <div v-if="!pending">
        <div class="kidsanna">
            <div class="container">
                <div class="kidsanna__wrapper">
                    <VueSlickCarousel class="carusel__sneakers" :arrows="true">
                        <div v-for="sneakers in colorData.sneakers" :key="sneakers.id" :id="sneakers.id"><img class="carusel__sneakers--logo" v-bind:src="sneakers.img" alt=""></div>
                    </VueSlickCarousel>
                    <div class="presence">
                        <div class="presence__head">
                            <div class="presence__head-instock" :class="colorData.presenceAvailable.class">{{colorData.presenceAvailable.title}}</div>
                            <div class="presence__head-vendorcode">{{colorData.presenceVendorCode}}</div>
                        </div>
                        <div class="presence__price">
                            <p class="presence__price-text--strike"><strike>{{colorData.priceProduct}}</strike><sub>грн</sub></p>
                            <p class="presence__price-text">{{colorData.productPriceDiscount}}<sub>грн</sub></p>
                        </div>
                        <label v-for="colors in viewsColor" :key="colors.id">
                            <input
                            :class="colors.class"
                            type="radio"
                            :id="colors.id"
                            name="age"
                            v-model="selectedСolor"
                            :value="colors.value"
                            />
                        </label>
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
        pending: "true",
        selectedСolor: "ColorRed",   
        viewsColor: [
            {
            id: 1,
            value: "ColorRed",
            class: "presence__colors-red"
            },
            {
            id: 2,
            value: "ColorGreen",
            class: "presence__colors-green"
            },
            {
            id: 3,
            value: "ColorOrange",
            class: "presence__colors-orange"
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
input[type=radio] {
    display: none;
}
.kidsanna {
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
    }

    &__color-red {
        background: red;
        border: 1px solid transparent;
        &:hover {
            background-color: #fff;
            border: 1px solid red;
            color: red;
        }
    }

    &__color-green {
        background: green;
        &:hover {
            background-color: #fff;
            border: 1px solid green;
            color: green;
        }
    }

    &__color-orange {
        background: orange;
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
    background-color: #ccc;
    margin-right: 20px;
    &--logo {
        object-fit: cover;
        object-position: center;
    }
}
button.slick-prev:before, 
button.slick-next:before {
    color: red !important;
}
.presence {
    width: 100%;
    &__head {
    display: flex;
    justify-content: space-between;
    align-items: center; 
    width: 100%;
    }
    &__head-instock {
        width: 97px;
        height: 30px;
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

</style>
