<template>
    <div v-if="!pending">
        <div class="kidsanna">
            <div class="container">
                <div class="kidsanna__wrapper">
                    <VueSlickCarousel class="carusel__items" v-bind="settings">
                        <div class="carusel__item" v-for="productItem in colorData.productItems" :key="productItem.id">
                            <img class="carusel__item-logo" :src="productItem.img" alt="">
                        </div>
                    </VueSlickCarousel>
                    <div class="info">
                        <div class="info__head">
                            <div class="info__head-instock" :class="{'not-in-stock': colorData.status !== 'В наличии' }">{{colorData.status}}</div>
                            <div class="info__head-vendorcode">Артикул: {{colorData.vendorCode}}</div>
                        </div>
                        <div class="price">
                            <p class="price__text--strike"><strike>{{colorData.priceProduct.value}}</strike><sub>{{colorData.priceProduct.currency}}</sub></p>
                            <p class="price__text">{{colorData.productPriceDiscount.value}}<sub>{{colorData.productPriceDiscount.currency}}</sub></p>
                        </div>
                        <div class="info__offer">
                            <h3 class="info__offer-title">Цвет:</h3>
                            <label v-for="colors in viewsColor" :key="colors.id">
                                <input
                                class="colors__select"
                                type="radio"
                                name="age"
                                :id="colors.id"
                                v-model="selectedСolor"
                                :value="colors.value"
                                @change="request(colors.id)"
                                />
                                <span class="colors__select" :style="{ backgroundColor: colors.color }"></span>
                            </label>
                        </div>
                        <button class="kidsanna__buy">Купить</button>
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
            color: '#DD292E'
            },
            {
            id: 2,
            value: "ColorGreen",
            color: '#2BA401'
            },
            {
            id: 3,
            value: "ColorOrange",
            color: '#FFB13C'
            },
        ],
        colorData: {},
    };
  },
  methods: {
    request: function(colorId){
            this.axios.get("./static/color"+colorId+".json")
            .then((response) => {
                this.colorData = response.data;
                this.pending = false;
            });
    }
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
@import url('https://fonts.googleapis.com/css2?family=Balsamiq+Sans:wght@700&family=Roboto:wght@400;500&display=swap');
body {
    background: #F5F5F5;
}

.container {
    max-width: 1260px;
    margin: 0 auto;
}

.carusel__items {
    width: 500px;
    margin-right: 30px;
    .carusel__item {
        height: 500px;
        &-logo {
            object-fit: cover;
            height: 500px;
        }
    }    
}

input[type="radio"] {
    display: none;
    
}
.colors__select {
    width: 30px;
    height: 30px;
    border-radius: 50%;
    display: inline-block;
    box-sizing: border-box;
    position: relative;
    cursor: pointer;
    margin-right: 5px;
    &:checked + &,
    &:checked + &,
    &:checked + & {
        width: 30px;
        height: 30px;
        border: 2px solid #F5F5F5;
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
    &:checked + &::before {
        opacity: 1;
    }
}


.kidsanna {
    max-width: 1260px;
    margin: 0 auto;
    font-family: 'Roboto', sans-serif;
    &__wrapper {
        display: flex;
    }
    &__buy {
        display: block;
        width: 210px;
        height: 50px;
        border-radius: 30px;
        font-weight: bold;
        font-size: 14px;
        line-height: 100%;
        text-transform: uppercase;
        color: #FFFFFF;
        transition: all .2s;
        cursor: pointer;
        background: red;
        border: 1px solid transparent;
        position: relative;
        padding-left: 20px;
        box-sizing: border-box;
        &::before {
            content: '';
            position: absolute;
            background-image: url('../../src/assets/images/basket.svg');
            width: 16px;
            height: 16px;
            left: 60px;
            top: 14px;
        }
    }
}

.info {
    max-width: 600px;
    width: 100%;
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
        border: 1px solid #F5F5F5;
        box-sizing: border-box;
        border-radius: 20px;
        display: flex;
        justify-content: center;
        align-items: center; 
        color: #00930F;
        &.not-in-stock {
            color: #F04137;
        }     
    } 
    &__head-vendorcode {
        font-size: 14px;
        line-height: 120%;
        color: #595959;     
    } 
    
    &__colors-red,
    &__colors-green,
    &__colors-orange {
        width: 30px;
        height: 30px;
    }

    &__offer {
        display: block;
        text-align: left;
        margin-bottom: 40px;
        &-title {
            font-weight: 500;
            font-size: 14px;
            line-height: 120%;
            color: #4F4F4F;
            margin: 0 0 20px 0;
        }
    }
}

.price {
    font-weight: bold;
    font-size: 30px;
    line-height: 100%;
    text-transform: uppercase;
    display: flex;
    justify-content: center;
    font-family: 'Balsamiq Sans', cursive;
    font-weight: bold;
    align-items: center;
    justify-content: flex-start;
    .price__text {    
        color: #F04137;
        font-weight: bold;
        font-size: 30px;
        line-height: 100%;
        text-transform: uppercase;
        margin: 30px 0;
        sub {
            font-size: 14px;
            line-height: 100%;
            font-family: 'Roboto', sans-serif;
        }
        &--strike {
            color: #828282;
            margin-right: 20px;
            font-weight: bold;
            font-size: 20px;
            line-height: 100%;
            text-transform: uppercase;
            color: #828282;
            sub {
                font-size: 14px;
                line-height: 100%;
                font-family: 'Roboto', sans-serif;
            }
        }
    }
}



</style>
<style lang="scss">
.slick-next:before {
    width: 31px;
    height: 32px;
    display: block;
    content: '';
    background-image: url('../../src/assets/images/arrow-right.svg');
    font-family: 'Roboto', sans-serif;
    background: #F5F5F5;
    opacity: 0.5;
    border-radius: 20px 0px 0px 20px;
}
.slick-prev::before {
    width: 31px;
    height: 32px;
    display: block;
    content: '';
    background-image: url('../../src/assets/images/arrow-right.svg');
    font-family: 'Roboto', sans-serif;
    background: #F5F5F5;
    opacity: 0.5;
    border-radius: 0px 20px 20px 0px;
}
.slick-next {
    right: 10px;
}

.slick-prev {
    left: 0px;
    z-index: 1;
}
</style>
