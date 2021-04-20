<template>
  <div class="kidsanna">
    <div class="container">
        <div class="kidsanna__wrapper">
            <VueSlickCarousel class="carusel-sneakers" :arrows="true">
            <div>1</div>
            <div>2</div>
            <div>3</div>
            <div>4</div>
            </VueSlickCarousel>
            <div class="presence">
                <div class="presence__head">
                    <div class="presence__head-instock">Вналичии</div>
                    <div class="presence__head-vendorcode">Артикул: 12633</div>
                </div>
                <div class="presence__price">
                    <p class="presence__price-text--strike"><strike>42 999грн</strike><sub>грн</sub></p>
                    <p class="presence__price-text">40 999<sub>грн</sub></p>
                </div>
                <label>
                    <input type="radio"/>
                </label>
                <button>Купить</button>
            </div>
        </div>
    </div>
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
    };
  },
};
</script>

<style scoped lang='scss'>
.kidsanna {
    &__wrapper {
    display: flex;
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
        color: #00930F;
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
}

</style>
