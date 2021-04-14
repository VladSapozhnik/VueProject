<template>
  <div class="order">
    <div class="order__forms">
      <h3>ФИО</h3>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.orderData.surname.value.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.orderData.surname.value.$model"
          :placeholder="orderData.surname.placeholder"
          :id="orderData.surname.id"
        />
        <div
          class="error"
          v-if="
            !$v.orderData.surname.value.required &&
            $v.orderData.surname.value.$dirty
          "
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="
            !$v.orderData.surname.value.minLength && orderData.surname.value
          "
        >
          Имя должно иметь не менее
          {{ $v.orderData.surname.value.$params.minLength.min }} символа.
        </div>
      </div>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.orderData.name.value.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.orderData.name.value.$model"
          :placeholder="orderData.name.placeholder"
          :id="orderData.name.id"
        />
        <div
          class="error"
          v-if="
            !$v.orderData.name.value.required && $v.orderData.name.value.$dirty
          "
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="!$v.orderData.name.value.minLength && orderData.name.value"
        >
          Имя должно иметь не менее
          {{ $v.orderData.name.value.$params.minLength.min }} символа.
        </div>
      </div>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.orderData.patronymic.value.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.orderData.patronymic.value.$model"
          :placeholder="orderData.patronymic.placeholder"
          :id="orderData.patronymic.id"
        />
        <div
          class="error"
          v-if="
            !$v.orderData.patronymic.value.required &&
            $v.orderData.patronymic.value.$dirty
          "
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="
            !$v.orderData.patronymic.value.minLength &&
            orderData.patronymic.value
          "
        >
          Имя должно иметь не менее
          {{ $v.orderData.patronymic.value.$params.minLength.min }} символа.
        </div>
      </div>
    </div>
    <div
      class="form-group"
      :class="{ 'form-group--error': $v.orderData.address.value.$error }"
    >
      <input
        class="order__forms-input"
        type="text"
        v-model="$v.orderData.address.value.$model"
        :placeholder="orderData.address.placeholder"
        :id="orderData.address.id"
      />
      <div
        class="error"
        v-if="
          !$v.orderData.address.value.required &&
          $v.orderData.address.value.$dirty
        "
      >
        Поле, обязательное для заполнения
      </div>
      <div
        class="error"
        v-if="!$v.orderData.address.value.minLength && orderData.address.value"
      >
        Имя должно иметь не менее
        {{ $v.orderData.address.value.$params.minLength.min }} символа.
      </div>
    </div>
    <div>
      <label v-for="ways in orderData.way.addressItems" :key="ways.id">
        <input
          name="mail"
          type="checkbox"
          v-model="ways.checked"
          :id="ways.id"
          :checked="ways.checked"
        />
        {{ ways.title }}
      </label>
      <div v-if="this.orderAddress == this.orderData.way.addressItems.checked">orderAddress</div>
    </div>
    <div>
      <select class="order__forms-select">
        <option
          v-for="newMail in orderData.newMail.addressItems"
          :value="newMail.value"
          :key="newMail.id"
          :id="newMail.id"
        >
          {{ newMail.title }}
        </option>
      </select>
    </div>
    <div>
      <select class="order__forms-select">
        <option
          v-for="ukrMail in orderData.ukrMail.addressItems"
          :value="ukrMail.value"
          :key="ukrMail.id"
          :id="ukrMail.id"
        >
          {{ ukrMail.title }}
        </option>
      </select>
    </div>
    <div :class="{ 'form-group--error': $v.orderData.pickup.value.$error }">
      <textarea
        v-model="$v.orderData.pickup.value.$model"
        :placeholder="orderData.pickup.placeholder"
        :id="orderData.pickup.id"
      >
      </textarea>
      <div
        class="error"
        v-if="
          !$v.orderData.pickup.value.required &&
          $v.orderData.pickup.value.$dirty
        "
      >
        Поле, обязательное для заполнения
      </div>
      <div
        class="error"
        v-if="!$v.orderData.pickup.value.minLength && orderData.pickup.value"
      >
        Имя должно иметь не менее
        {{ $v.orderData.pickup.value.$params.minLength.min }} символа.
      </div>
    </div>
    <button class="order__forms-btn">Отправить</button>
  </div>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";
export default {
  name: "order",
  data: function () {
    return {
      orderAddress: false,
      orderData: {
        surname: {
          id: 1,
          value: "Hifffff",
          placeholder: "Фамилия",
          title: "Фамилия",
        },
        name: {
          id: 2,
          value: "",
          placeholder: "Имя",
        },
        patronymic: {
          id: 3,
          value: "",
          placeholder: "Отчество",
        },
        address: {
          id: 4,
          value: "",
          placeholder: "Адрес",
        },
        way: {
          addressItems: [
            {
              id: 5,
              value: "NewMaill",
              title: "Новая Почта",
              checked: true
            },
            {
              id: 6,
              value: "UkrMail",
              title: "Укр Почта",
              checked: false
            },
            {
              id: 7,
              value: "pickup",
              title: "Самовывоз",
              checked: false
            },
          ],
        },
        newMail: {
          checked: "",
          addressItems: [
            {
              id: 8,
              value: "Poltava",
              title: "Poltava",
            },
            {
              id: 9,
              value: "Nikolaev",
              title: "Nikolaev",
            },
            {
              id: 10,
              value: "Odessa",
              title: "Odessa",
            },
          ],
        },
        ukrMail: {
          checked: "",
          addressItems: [
            {
              id: 8,
              value: "Poltava-1",
              title: "Poltava-2",
            },
            {
              id: 9,
              value: "Nikolaev-2",
              title: "Nikolaev-2",
            },
            {
              id: 10,
              value: "Odessa-3",
              title: "Odessa-3",
            },
          ],
        },
        pickup: {
          id: 11,
          value: "",
          placeholder: "Введите ваши данные",
        },
      },
    };
  },
  validations: {
    orderData: {
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
      address: {
        value: {
          required,
          minLength: minLength(6),
        },
      },
      pickup: {
        value: {
          required,
          minLength: minLength(8),
        },
      },
    },
  },
  methods: {},
  watch: {
    orderData: {
      handler: function (vue) {
        console.log(vue);
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

.form-group {
  padding-bottom: 15px;
  box-sizing: border-box;
}

.error {
  color: rgb(196, 56, 56);
  font-size: 11px;
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