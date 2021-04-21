<template>
    <div v-if="!pending">
        <div class="kidsanna">
            <div class="container">
                <div class="kidsanna__wrapper">
                    <VueSlickCarousel v-for="sneakers in colorData.sneakers" :key="sneakers.id" class="carusel-sneakers" :arrows="true">
                        <div :id="sneakers.id">{{sneakers.title}}</div>
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
                        <button class="kidsanna__product-buy">Купить</button>
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
        selectedСolor: "colorRed",   
        viewsColor: [
            {
            id: 1,
            value: "colorRed",
            "class": "presence__colors-red"
            },
            {
            id: 2,
            value: "colorGreen",
            "class": "presence__colors-green"
            },
            {
            id: 3,
            value: "colorOrange",
            "class": "presence__colors-orange"
            },
        ],
        ColorData: {}
    };
  },
  methods: {
  },
  watch: {
    selectedСolor: {
      handler: function (val) {
        console.log(val);
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
.kidsanna {
    &__wrapper {
        display: flex;
    }
    &__product-buy {
        display: block;
        width: 210px;
        height: 50px;
        margin: 20px auto 0;
        background: #F04137;
        border: none;
        border-radius: 30px;
        font-weight: bold;
        font-size: 14px;
        line-height: 100%;
        text-transform: uppercase;
        color: #FFFFFF;
    }
}

.container {
    max-width: 1260px;
    margin: 0 auto;
}

.carusel-sneakers {
    width: 504px;
    height: 482px;
    background-color: #ccc;
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
