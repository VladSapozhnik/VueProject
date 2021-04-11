<template>
  <div class="forms">
    <div v-if="!pending">
      <div class="form-inner">
        <pre>{{ $v.personalForm.name.value }}</pre>
        <input
          v-model="personalForm.name.value"
          class="forms-text"
          :id="personalForm.name.id"
          :class="{
            'is-invalid': $v.personalForm.name.value.$error,
            redInput: $v.personalForm.name.value.$error,
          }"
          type="text"
          :placeholder="personalForm.name.placeholder"
          @blur="$v.personalForm.name.value.$touch()"
        />

        <input
          v-model="personalForm.tel.value"
          class="forms-text"
          :id="personalForm.tel.id"
          type="tel"
          :placeholder="personalForm.tel.placeholder"
        />

        <input
          v-model="personalForm.email.value"
          class="forms-text"
          type="email"
          :id="personalForm.email.id"
          name="email"
          :placeholder="personalForm.email.placeholder"
        />

        <div class="radio-offer">
          <h3>Сколько вам лет?</h3>
          <label v-for="age in personalForm.age" :key="age.id">
            <input class="radio" type="radio" :id="age.id" :value="age.value" />
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
      <div>
        <h3>Комментарии</h3>
        <textarea
          v-model="personalForm.messageArea.value"
          :id="personalForm.messageArea.id"
          :placeholder="personalForm.messageArea.placeholder"
        ></textarea>
      </div>
    </div>
    <div v-if="pending">ПРЕЛОАДЕР</div>
  </div>
</template>

<script>
import { required, minLength } from "vuelidate/lib/validators";
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
          minLength: minLength(4),
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
    // formsRegistration: {
    //   handler: function (val) {
    //     console.log(val);
    //   },
    //   deep: true,
    // },
  },
};
</script>

<style scoped lang="scss">
.redInput {
  background-color: #ab5f61;
  color: #fff;
  &::placeholder {
    color: #fff;
  }
  &:focus {
    border: 1px solid #fff;
  }
}

input:focus,
input:active {
  border: none;
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
}
</style>