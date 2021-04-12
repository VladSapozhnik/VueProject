<template>
  <div class="order">
    <div v-if="!pending">
        <div class="">
            <label>
                <span>Фамилия</span>
                <input type="text"
                v-model="orderForm.surname.value"
                :placeholder="orderForm.surname.placeholder"
                :id="orderForm.surname.id"
                />
            </label>
            <label>
                <span>Имя</span>
                <input type="text"
                v-model="orderForm.name.value"
                :placeholder="orderForm.name.placeholder"
                :id="orderForm.name.id"
                />
            </label>
            <label>
                <span>Отчество</span>
                <input type="text"
                v-model="orderForm.patronymic.value"
                :placeholder="orderForm.patronymic.placeholder"
                :id="orderForm.patronymic.id"
                />
            </label>
        </div>
        <div class="radio-offer">
            <h3>Способ доставки</h3>
            <label v-for="mail in orderForm.way.addressItems" :key="mail.id">
                <input 
                class="radio" 
                type="radio"
                name="mail"
                :id="mail.id"
                :value="mail.value"
                />
                <span>{{mail.title}}</span>
            </label>     
        </div>
        <div>
            <select>
                <option></option>
            </select>
            <select>
                <option></option>
            </select>
            <textarea>

            </textarea>
        </div>
    </div>
<!--     <div v-if="pending">ПРЕЛОАДЕР</div> -->
  </div>
</template>

<script>
/* import { required, minLength, email } from "vuelidate/lib/validators"; */
export default {
  name: "order",
  data: function () {
    return {
      orderForm: {},
      pending: true,
    };
  },
    created: function () {
    this.axios.get("./static/order.json").then((response) => {
      this.orderForm = response.data;
      this.pending = false;
      console.log(this.orderForm);
    });
  },
  watch: {
    orderForm: {
      handler: function (val) {
        console.log(val);
        /* console.log(this.$v) */
      },
      deep: true,
    },
  },
};
</script>

<style scoped lang="scss">

</style>