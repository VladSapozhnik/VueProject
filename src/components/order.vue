<template>
  <div class="order">
    <div v-if="!pending">
      <div class="order__forms">
        <h3>ФИО</h3>
        <div
          class="form-group"
          :class="{ 'form-group--error': $v.surname.value.$error }"
        >
          <input
            type="text"
            v-model="$v.surname.value.$model"
            :placeholder="surname.placeholder"
            :id="surname.id"
            class="order__forms-input"
          />
          <div
            class="error"
            v-if="
              !$v.surname.value.required &&
              $v.surname.value.$dirty"
          >
            Поле, обязательное для заполнения
          </div>
          <div
            class="error"
            v-if="
              !$v.surname.value.minLength &&
              $v.surname.value.$dirty"
          >          
            Введите не менее
            {{ $v.surname.value.$params.minLength.min }} символов.
          </div>
        </div>
        <div
          class="form-group"
          :class="{ 'form-group--error': $v.name.value.$error }"
        >
          <input
            type="text"
            v-model="$v.name.value.$model"
            :placeholder="name.placeholder"
            :id="name.id"
            class="order__forms-input"
          />
          <div
            class="error"
            v-if="
              !$v.name.value.required &&
              $v.name.value.$dirty"
          >
            Поле, обязательное для заполнения
          </div>
          <div
            class="error"
            v-if="
              !$v.name.value.minLength &&
              $v.name.value.$dirty"
          >
            Введите не менее
            {{ $v.name.value.$params.minLength.min }} символов.
          </div>
        </div>
        <div
          class="form-group"
          :class="{ 'form-group--error': $v.patronymic.value.$error }"
        >
          <input
            type="text"
            v-model="$v.patronymic.value.$model"
            :placeholder="patronymic.placeholder"
            :id="patronymic.id"
            class="order__forms-input"
          />
          <div
            class="error"
            v-if="
              !$v.patronymic.value.required &&
              $v.patronymic.value.$dirty"
          >
            Поле, обязательное для заполнения
          </div>
          <div
            class="error"
            v-if="
              !$v.patronymic.value.minLength &&
              $v.patronymic.value.$dirty"
          >
            Введите не менее
            {{ $v.surname.value.$params.minLength.min }} символов.
          </div>
        </div>
      </div>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.patronymic.value.$error }"
      >
        <h3>Адрес</h3>
        <input
          type="text"
          v-model="$v.address.value.$model"
          :placeholder="address.placeholder"
          :id="address.id"
          class="order__forms-input"
        />
        <div
          class="error"
          v-if="
            !$v.address.value.required &&
            $v.address.value.$dirty"
        >
          Поле, обязательное для заполнения
        </div>
      </div>
      <div class="order__radio tabs">
        <h3>Способ доставки</h3>
        <label v-for="mail in way.addressItems" :key="mail.id">
          <input
            class="radio"
            type="radio"
            name="mail"
            :id="mail.id"
            :value="mail.value"
            v-model="mail.checked"
          />
          <span>{{ mail.title }}</span>
        </label>
      </div>
      <div>
        <select v-if="way.addressItems.value = 'NewMail'" class="order__forms-select">
          <option
            v-for="newMail in newMail.addressItems"
            :key="newMail.id"
            :value="newMail.value"
            :id="newMail.id"
          >
            {{ newMail.title }}
          </option>
        </select>
        <select class="order__forms-select">
          <option
            class="order__forms-select"
            v-for="ukrMail in orderForm.ukrMail.addressItems"
            :key="ukrMail.id"
            :value="ukrMail.value"
            :id="ukrMail.id"
          >
            {{ ukrMail.title }}
          </option>
        </select>
        <div
          class="form-group"
          :class="{ 'form-group--error': $v.pickup.value.$error }"
        >
          <textarea
            :placeholder="pickup.placeholder"
            :id="pickup.id"
            v-model="$v.pickup.value.$model"
          >
          </textarea>
          <div
            class="error"
            v-if="
              !$v.pickup.value.required &&
              $v.pickup.value.$dirty"
          >
            Поле, обязательное для заполнения
          </div>
        </div>
      </div>
      <button class="order__forms-btn">Отправить</button>
    </div>
    <!--     <div v-if="pending">ПРЕЛОАДЕР</div> -->
  </div>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";
export default {
  name: "order",
  data: function () {
    return {
      pending: true,
      surname: {
        "id": 1,
        "value": "Hifffff",
        "placeholder": "Фамилия",
        "title": "Фамилия"
      },
      name: {
          "id": 2,
          "value": "",
          "placeholder": "Имя"
      },
      patronymic: {
          "id": 3,
          "value": "",
          "placeholder": "Отчество"
      },
      address: {
          "id": 4,
          "value": "",
          "placeholder": "Адрес"
      },
      way: {
          "addressItems": [    
              {
                  "id": 5,
                  "value": "NewMail",
                  "title": "Новая Почта",
                  "checked": "NewMail"
              },
              {
                  "id": 6,
                  "value": "UkrMail",
                  "title": "Укр Почта",
                  "checked": "UkrMail"
              },
              {
                  "id": 7,
                  "value": "pickup",
                  "title": "Самовывоз",
                  "checked": "pickup"
              }
          ]
      },
      newMail: {
          "checked": "",
          "addressItems": [    
              {
                  "id": 8,
                  "value": "Poltava",
                  "title": "Poltava"
              },
              {
                  "id": 9,
                  "value": "Nikolaev",
                  "title": "Nikolaev"
              },
              {
                  "id": 10,
                  "value": "Odessa",
                  "title": "Odessa"
              }
          ]
      },
      ukrMail: {
          "checked": "",
          "addressItems": [    
              {
                  "id": 8,
                  "value": "Poltava-1",
                  "title": "Poltava-2"
              },
              {
                  "id": 9,
                  "value": "Nikolaev-2",
                  "title": "Nikolaev-2"
              },
              {
                  "id": 10,
                  "value": "Odessa-3",
                  "title": "Odessa-3"
              }
          ]
      },
      pickup: {
          "id": 11,
          "value": "",
          "placeholder": "Введите ваши данные"
      }
    };
  },
  methods: {

  },
  validations: {
    surname: {
        value: {
          required,
          minLength: minLength(6),
        },
    },
    name: {
      value: {
        required,
        minLength: minLength(6),
      },
    },
    patronymic: {
      value: {
        required,
        minLength: minLength(6),
      },
    },
    pickup: {
      value: {
        required,
      },
    },
    address: {
      value: {
        required,
      },
    },
  },
  created: function () {
    this.axios.get("./static/order.json").then((response) => {
      this.orderForm = response.data;
      this.pending = false;
    });
  },
  watch: {
    orderForm: {
      handler: function (val) {
        console.log(val);
      },
      deep: true,
    },
  },
};
</script>

<style scoped lang="scss">
.order {
  max-width: 900px;
  margin: 0 auto;
  border: 1px solid #000;
  padding: 50px 0;
}

.error {
  color: rgb(196, 56, 56);
}

.order__forms {
  display: flex;
  justify-content: space-around;
  align-items: center;
  &-input,
  &-select {
    width: 200px;
    height: 30px;
    padding-left: 10px;
    border: none;
    outline: none;
    border-bottom: 1px solid #000;
    margin: 0 10px 10px 0;
  }
  &-btn {
    width: 150px;
    height: 40px;
    border: none;
    background-color: #000;
    color: #fff;
  }
}

textarea {
  width: 300px;
  min-height: 200px;
  resize: none;
  padding: 10px;
  outline: none;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>