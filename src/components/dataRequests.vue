<template>
  <div>
    <div class="requests-btn" @click="requestData">Open Requests</div> <!-- При клике вызываем функцию -->
    <ul v-if="visibleResult.length > 0" class="requests-list"> <!-- если массив равен больше 0 -->
      <li v-for="requestItem in visibleResult" :key="requestItem.id">{{requestItem.id}}, {{requestItem.title}}</li>
    </ul>
    <div @click="evenMake" v-if="visibleResult.length > 0" class="requests-btn">четные</div>
    <div @click="oddMake" v-if="visibleResult.length > 0" class="requests-btn">нечетные</div>
    <div @click="modMake" v-if="visibleResult.length > 0" class="requests-btn">Модификация</div>
    <div @click="cancel" v-if="visibleResult.length > 0" class="requests-btn">отмена</div>
  </div>
</template>

<script>
export default {
  name: 'Requests',

  data: function() {
      return {
          requestResult: [], // пустой массив куда будем ложить данные
          visibleResult: [] // пустой массив куда ложим измененный масив, что выше
      }    
  },
  methods: {
      evenMake: function () {
          this.visibleResult = this.requestResult.filter(item => item.value % 2 === 0) //выводить четные числа, visibleResult новый массив куда мы кладем четные числа из массива requestResult
      },
      oddMake: function () {
          this.visibleResult = this.requestResult.filter(item => item.value % 2 !== 0) //выводить нечетные числа, visibleResult новый массив куда мы кладем нечетные числа из массива requestResult
      },
      modMake: function () {
          console.log(this.requestResult)
         console.log(this.visibleResult)
          this.visibleResult = this.requestResult.map(item =>  {
              return {...item,  title: item.title + '5'  }
          })
          console.log(this.requestResult)
         console.log(this.visibleResult)
      },
      requestData: function () { // <-- функция для axios
        this.axios
            .get('./static/test.json')
            .then(response => {
            this.requestResult = response.data // <-- кладем в массив данные
            this.visibleResult = this.requestResult
        })
      },
      cancel: function(){
          this.visibleResult = this.requestResult; //кладем в функцию данные которые были в начале.
      }
  },
}
</script>

<style scoped lang='scss'>
    ul {
        width: 300px;
        border: 1px solid #000;
        list-style-type: none;
        padding: 10px 0;
        margin: 0 auto;
        background-color: rgb(61, 163, 170); 
        color: #fff;
        border-radius: 20px;
    }

    li {
        padding-top: 5px;
        padding-bottom: 5px;
    }
    .requests-btn {
        width: 200px;
        height: 50px;
        background-color: rgb(61, 163, 170); 
        border: none;
        border-radius: 10px;
        color: #fff;
        outline: none;
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 50px auto 10px;
        cursor: pointer;
    }
</style>