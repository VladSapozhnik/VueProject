<template>
  <div class="order">
    <div class="order__forms">
      <h3>ФИО</h3>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.orderData.surname.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.orderData.surname.$model"
          placeholder="Введите фамилию"
        />
        <div
          class="error"
          v-if="!$v.orderData.surname.required && $v.orderData.surname.$dirty"
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="!$v.orderData.surname.minLength && orderData.surname"
        >
          Имя должно иметь не менее
          {{ $v.orderData.surname.$params.minLength.min }} символа.
        </div>
      </div>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.orderData.name.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.orderData.name.$model"
          placeholder="Введите имя"
        />
        <div
          class="error"
          v-if="!$v.orderData.name.required && $v.orderData.name.$dirty"
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="!$v.orderData.name.minLength && orderData.name"
        >
          Имя должно иметь не менее
          {{ $v.orderData.name.$params.minLength.min }} символа.
        </div>
      </div>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.orderData.patronymic.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.orderData.patronymic.$model"
          placeholder="Отчество"
        />
        <div
          class="error"
          v-if="
            !$v.orderData.patronymic.required && $v.orderData.patronymic.$dirty
          "
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="!$v.orderData.patronymic.minLength && orderData.patronymic"
        >
          Имя должно иметь не менее
          {{ $v.orderData.patronymic.$params.minLength.min }} символа.
        </div>
      </div>
    </div>
    <div
      class="form-group"
      :class="{ 'form-group--error': $v.orderData.address.$error }"
    >
      <input
        class="order__forms-input"
        type="text"
        v-model="$v.orderData.address.$model"
        placeholder="address vvedite"
      />
      <div
        class="error"
        v-if="!$v.orderData.address.required && $v.orderData.address.$dirty"
      >
        Поле, обязательное для заполнения
      </div>
      <div
        class="error"
        v-if="!$v.orderData.address.minLength && orderData.address"
      >
        Имя должно иметь не менее
        {{ $v.orderData.address.$params.minLength.min }} символа.
      </div>
    </div>
    <div>
      <label v-for="ways in deliveryTypes" :key="ways.id">
        <input
          name="ways"
          type="radio"
          :value="ways.value"
          :id="ways.id"
          v-model="orderData.way"
        />
        {{ ways.title }}
      </label>
    </div>
    <div v-if="this.orderData.way == 'NewMail'">
      <select class="order__forms-select" v-model="orderData.newMail">
        <option
          v-for="newMail in newPostDepartments"
          :value="newMail.value"
          :key="newMail.id"
          :id="newMail.id"
        >
          {{ newMail.title }}
        </option>
      </select>
    </div>
    <div v-if="this.orderData.way == 'UkrMail'">
      <select class="order__forms-select" v-model="orderData.UkrMail">
        <option
          v-for="ukrMail in UkrMailDepartments"
          :value="ukrMail.value"
          :key="ukrMail.id"
          :id="ukrMail.id"
        >
          {{ ukrMail.title }}
        </option>
      </select>
    </div>
    <div
      v-if="this.orderData.way == 'orderDescription'"
      :class="{ 'form-group--error': $v.orderData.orderDescription.$error }"
    >
      <textarea
        v-model="$v.orderData.orderDescription.$model"
        placeholder="Напишите комментарий"
      >
      </textarea>
      <div
        class="error"
        v-if="
          !$v.orderData.orderDescription.required &&
          $v.orderData.orderDescription.$dirty"
      >
        Поле, обязательное для заполнения
      </div>
      <div
        class="error"
        v-if="
          !$v.orderData.orderDescription.minLength && orderData.orderDescription"
      >
        Имя должно иметь не менее
        {{ $v.orderData.orderDescription.$params.minLength.min }} символа.
      </div>
    </div>
    <button @click="sendForms" class="order__forms-btn">Отправить</button>
  </div>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";
export default {
  name: "order",
  data: function () {
    return {
      deliveryTypes: [
        {
          id: 5,
          value: "NewMail",
          title: "Новая Почта",
        },
        {
          id: 6,
          value: "UkrMail",
          title: "Укр Почта",
        },
        {
          id: 7,
          value: "orderDescription",
          title: "Самовывоз",
        },
      ],
      newPostDepartments: [
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
      UkrMailDepartments: [
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
      orderData: {
        surname: "",
        name: "",
        patronymic: "",
        address: "",
        way: "UkrMail",
        newMail: "",
        ukrMail: "",
        orderDescription: "",
      },
    };
  },
  validations: {
    orderData: {
      surname: {
        required,
        minLength: minLength(6),
      },
      name: {
        required,
        minLength: minLength(6),
      },
      patronymic: {
        required,
        minLength: minLength(6),
      },
      address: {
        required,
        minLength: minLength(6),
      },
      orderDescription: {
        required,
        minLength: minLength(8),
      },
    },
  },
  methods: {
    sendForms: function () {
      //   /*     this.axios.get("http//").then((response) => {
      //   this.orderData = response.data;
      //   console.log(this.orderData);
      // }); */
      this.axios
        .post("/asdasdasd", {
          firstName: "Fred",
          lastName: "Flintstone",
          orderData: {
            surname: "",
            name: this.name.data,
            patronymic: "",
            address: "",
            way: "",
            newMail: "",
            ukrMail: "",
            orderDescription: "",
          }
        })
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
  },
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