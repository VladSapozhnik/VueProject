<template>
  <div class="order">
    <div class="order__forms">
      <h3>ФИО</h3>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.userData.surname.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.userData.surname.$model"
          placeholder="Введите фамилию"
        />
        <div
          class="error"
          v-if="!$v.userData.surname.required && $v.userData.surname.$dirty"
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="!$v.userData.surname.minLength && userData.surname"
        >
          Имя должно иметь не менее
          {{ $v.userData.surname.$params.minLength.min }} символа.
        </div>
      </div>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.userData.name.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.userData.name.$model"
          placeholder="Введите имя"
        />
        <div
          class="error"
          v-if="!$v.userData.name.required && $v.userData.name.$dirty"
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="!$v.userData.name.minLength && userData.name"
        >
          Имя должно иметь не менее
          {{ $v.userData.name.$params.minLength.min }} символа.
        </div>
      </div>
      <div
        class="form-group"
        :class="{ 'form-group--error': $v.userData.patronymic.$error }"
      >
        <input
          class="order__forms-input"
          type="text"
          v-model="$v.userData.patronymic.$model"
          placeholder="Отчество"
        />
        <div
          class="error"
          v-if="
            !$v.userData.patronymic.required && $v.userData.patronymic.$dirty
          "
        >
          Поле, обязательное для заполнения
        </div>
        <div
          class="error"
          v-if="!$v.userData.patronymic.minLength && userData.patronymic"
        >
          Имя должно иметь не менее
          {{ $v.userData.patronymic.$params.minLength.min }} символа.
        </div>
      </div>
    </div>
    <div
      class="form-group"
      :class="{ 'form-group--error': $v.userData.address.$error }"
    >
      <input
        class="order__forms-input"
        type="text"
        v-model="$v.userData.address.$model"
        placeholder="address vvedite"
      />
      <div
        class="error"
        v-if="!$v.userData.address.required && $v.userData.address.$dirty"
      >
        Поле, обязательное для заполнения
      </div>
      <div
        class="error"
        v-if="!$v.userData.address.minLength && userData.address"
      >
        Имя должно иметь не менее
        {{ $v.userData.address.$params.minLength.min }} символа.
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
      <select class="order__forms-select" v-model="orderData.ukrMail">
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
          title: "Отделение №1",
        },
        {
          id: 9,
          value: "Nikolaev",
          title: "Отделение №2",
        },
        {
          id: 10,
          value: "Odessa",
          title: "Отделение №3",
        },
      ],
      UkrMailDepartments: [
        {
          id: 8,
          value: "Poltava-1",
          title: "Отделение №1",
        },
        {
          id: 9,
          value: "Nikolaev-2",
          title: "Отделение №2",
        },
        {
          id: 10,
          value: "Odessa-3",
          title: "Отделение №3",
        },
      ],
      orderData: {
        way: "",
        newMail: "",
        ukrMail: "",
        orderDescription: "",
      },
      deliveryData: {},
      userData: {
        surname: "asdasda",
        name: "",
        patronymic: "",
        address: "",
      }
    };
  },
  validations: {
    userData: {
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
    },
    orderData: {
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
        .post("/asdasdasd", Object.assign(this.deliveryData, this.userData))
        .then(function (response) {
          console.log(response);
        })
        .catch(function (error) {
          console.log(error);
        });
    },
    orderForms: function () {
      this.orderData = []
    }
  },
  watch: {
    orderData: {
      handler: function (value) { 
  /*       Object.assign(this.orderData, this.userData) */
        if (value.way == 'NewMail') {
          console.log('НОВАЯ ПОЧТА')
          this.deliveryData = {
            devilereType:value.way,
            postOffice:value.newMail,
          }
        }
        else if (value.way == 'UkrMail') {
          console.log('УКР ПОЧТА')
          this.deliveryData = {
            devilereType:value.way,
            postOffice:value.ukrMail,
          }
        }
        else if (value.way == 'orderDescription') {
          console.log('САМОВЫВОЗ')
          this.deliveryData = {
            devilereType:value.way,           
            comment:value.orderDescription,
          }
        }
      },
      deep: true,
    },
    userData: {
      handler: function (valueData) {
        console.log(valueData);
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