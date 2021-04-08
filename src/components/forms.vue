<template>
  <div class="forms">
    <div class="form-inner">
        <input v-model="formsRegistration.name" class="forms-text" placeholder="Имя"/>
        <input v-model="formsRegistration.tel" class="forms-text" type="tel" id="phone" name="phone" placeholder="Телефон"/>
        <input v-model="formsRegistration.email" class="forms-text" type="email" id="email" name="email" placeholder="Email"/>
        <div class="checkbox">
          <h3>Какие животные у вас есть?</h3>
          <div class="checkbox-name">
            <input v-model="formsRegistration.pets" type="checkbox" id="dog" value="dog" />
            <label for="dog">Собака</label>
            <input v-model="formsRegistration.pets" type="checkbox" id="Cat" value="Cat" />
            <label for="Cat">Кот</label>
            <input v-model="formsRegistration.pets" type="checkbox" id="mouse" value="mouse" />
            <label for="mouse">Мышь</label>
          </div>
        </div>
        <div class="radio-offer">
          <h3>Сколько вам лет?</h3>
          <input class="radio" v-model="formsRegistration.age" type="radio" id="One" value="18" />
          <label for="One">18</label>

          <input class="radio" v-model="formsRegistration.age" type="radio" id="Two" value="19" />
          <label for="Two">19</label>

          <input class="radio" v-model="formsRegistration.age" type="radio" id="Three" value="20" />
          <label for="Three">20</label>
        </div>
    </div>
    <div>
      <textarea v-model="formsRegistration.messageArea" placeholder="Textarea"></textarea>
    </div>
  </div>
</template>

<script>
export default {
  name: 'forms',
   data: function() {
      return {
          formsRegistration: {
            name: '',
            tel: '',
            email: '',
            pets: [],
            age: '',
            messageArea: '',
          },
      }    
  },

  watch: {
    formsRegistration: {
            handler: function(val) {
               console.log(val)
            },
            deep: true
        }
  }
}
</script>

<style scoped>
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