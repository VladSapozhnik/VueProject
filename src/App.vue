<template>
  <div id="app">
    <!-- <HelloWorld />
    <popup/>
      <template v-slot:title> Это тайтл </template>
      <template v-slot:result> Это резалт </template>
    </popup> -->
    <!-- <Requests /> -->
    <!-- <hr /> -->
    <!-- <forms /> -->
    <!-- <order/> -->
    <kidsanna/>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
// import popup from "./components/Popup.vue";
// import Requests from "./components/dataRequests.vue";
/* import forms from "./components/forms.vue"; */
/* import order from "./components/order.vue" */
import kidsanna from "./components/kidsanna.vue"

export default {
  name: "App",
  components: {
    // HelloWorld,
    // popup,
    // Requests,
    /* forms, */
/*     order, */
    kidsanna
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
