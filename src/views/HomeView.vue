<template>
  <div class="main-container">
    <Banner />
    <h1>Make U Burger</h1>
    <BurgerForm />
  </div>
</template>

<script>
import BurgerForm from "../components/BurgerForm.vue";
import Banner from "../components/Banner.vue";

export default {
  name: "HomeView",
  components: {
    Banner,
    BurgerForm,
  },
};
</script>
