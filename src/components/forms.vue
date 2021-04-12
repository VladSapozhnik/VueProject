<template>
  <div class="forms">
    <div v-if="!pending">
      <div class="form-inner">
        <div
          class="form-group"
          :class="{ 'form-group--error': $v.personalForm.name.value.$error }"
        >
          <input
            v-model="$v.personalForm.name.value.$model"
            class="forms-text"
            :id="personalForm.name.id"
            type="text"
            :placeholder="personalForm.name.placeholder"
          />
        </div>
        <div class="error" v-if="!$v.personalForm.name.value.required && $v.personalForm.name.value.$dirty">
          Поле, обязательное для заполнения
        </div>
        <div class="error" v-if="!$v.personalForm.name.value.minLength && $v.personalForm.name.value.$dirty">
          Имя должно иметь не менее
          {{ $v.personalForm.name.value.$params.minLength.min }} символа.
        </div>
        <div
          class="form-group"
          :class="{ 'form-group--error': $v.personalForm.tel.value.$error }"
        >
          <input
            v-model="$v.personalForm.tel.value.$model"
            class="forms-text"
            :id="personalForm.tel.id"
            type="tel"
            :placeholder="personalForm.tel.placeholder"
          />
        </div>
        <div class="error" v-if="!$v.personalForm.tel.value.required && $v.personalForm.tel.value.$dirty">
          Поле, обязательное для заполнения
        </div>
        <div class="error" v-if="!$v.personalForm.tel.value.minLength && $v.personalForm.tel.value.$dirty">
          Номер должен иметь не менее
          {{ $v.personalForm.tel.value.$params.minLength.min }} символа.
        </div>
        <div class="error" v-if="!$v.personalForm.tel.value.numeric && $v.personalForm.tel.value.$dirty">
          Можно вводить только цифры!
        </div>

        <div
          class="form-group"
          :class="{ 'form-group--error': $v.personalForm.email.value.$error }"
        >
          <input
            v-model="$v.personalForm.email.value.$model"
            class="forms-text"
            type="email"
            :id="personalForm.email.id"
            name="email"
            :placeholder="personalForm.email.placeholder"
          />
          <div class="error" v-if="!$v.personalForm.email.value.required && $v.personalForm.email.value.$dirty">
            Поле, обязательное для заполнения
          </div>
          <div class="error" v-if="!$v.personalForm.email.value.email && $v.personalForm.email.value.$dirty">
            Введите корректный Email
          </div>
        </div>

        <div class="radio-offer">
          <h3>Сколько вам лет?</h3>
          <label v-for="age in personalForm.age.items" :key="age.id">
            <input
              class="radio"
              type="radio"
              :id="age.id"
              name="age"
              v-model="personalForm.age.checked"
              :value="age.value"
            />
            <span>{{ age.title }}</span>
          </label>
        </div>

        <div class="checkbox">
          <h3>Какие животные у вас есть?</h3>
          <div class="checkbox-name">
            <label v-for="pets in personalForm.pets" :key="pets.id">
              <input
                v-model="pets.checked"
                :value="pets.value"
                :id="pets.id"
                type="checkbox"
              />
              <span>{{ pets.title }}</span>
            </label>
          </div>
        </div>
      </div>
      <div
        :class="{
          'form-group--error': $v.personalForm.messageArea.value.$error,
        }"
      >
        <h3>Комментарии</h3>
        <textarea
          v-model="$v.personalForm.messageArea.value.$model"
          :id="personalForm.messageArea.id"
          :placeholder="personalForm.messageArea.placeholder"
        ></textarea>
      </div>
      <div class="error" v-if="!$v.personalForm.messageArea.value.required && $v.personalForm.messageArea.value.$dirty">
        Поле, обязательное для заполнения
      </div>
      <div class="error" v-if="!$v.personalForm.messageArea.value.minLength && $v.personalForm.messageArea.value.$dirty">
        Имя должно иметь не менее
        {{ $v.personalForm.messageArea.value.$params.minLength.min }} символа.
      </div>
    </div>
    <div v-if="pending">ПРЕЛОАДЕР</div>
  </div>
</template>

<script>
import { required, minLength, email } from "vuelidate/lib/validators";
export default {
  name: "forms",
  data: function () {
    return {
      personalForm: {},
      pending: true,
    };
  },
  validations: {
    personalForm: {
      name: {
        value: {
          required,
          minLength: minLength(6),
        },
      },
      tel: {
        value: {
          required,
          minLength: minLength(11),
        },
      },
      email: {
        value: {
          required,
          minLength: minLength(6),
          email,
        },
      },
      messageArea: {
        value: {
          required,
          minLength: minLength(8),
        },
      },
    },
  },
  created: function () {
    this.axios.get("./static/form.json").then((response) => {
      this.personalForm = response.data;
      this.pending = false;
      console.log(this.personalForm);
    });
    // запрос axios
    // результат кладем в персонал форм.
  },

  watch: {
    personalForm: {
      handler: function (val) {
        console.log(val);
        console.log(this.$v)
      },
      deep: true,
    },
  },
};
</script>

<style scoped lang="scss">
input {
  outline: none;
}
.form-group--error {
  outline: outline-color;
}

.error {
  color: rgb(196, 56, 56);
  padding-bottom: 5px;
}

.forms {
  max-width: 730px;
  min-height: 350px;
  background-color: rgb(61, 163, 170);
  margin: 0 auto;
  border-radius: 10px;
  padding: 50px;
  display: flex;
  justify-content: space-between;
}

.form-inner {
  display: flex;
  flex-direction: column;
}

.forms-text {
  width: 300px;
  height: 40px;
  padding: 0 10px;
  border-radius: 5px;
  border: none;
  margin-bottom: 10px;
}

.forms-checkbox {
  width: 20px;
  height: 20px;
}

.checkbox {
  max-width: 300px;
}

.checkbox-name {
  display: flex;
  justify-content: space-between;
  width: 100px;
}

.checkbox-span {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 300px;
  height: 40px;
  border: 1px solid #000;
}

.checkbox-name {
  width: 200px;
  height: 20px;
  border-radius: 10px;
  display: flex;
  margin: 0 auto;
}

.radio-offer {
  display: flex;
  align-items: center;
  margin-top: 30px;
}

.radio {
  width: 15px;
  height: 15px;
}

select {
  width: 150px;
  height: 30px;
  margin: 30px 0 10px;
}

textarea {
  width: 300px;
  min-height: 200px;
  resize: none;
  padding: 10px;
  border-radius: 10px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
</style>