<template>
  <div class="main-banner">
    <h1 class="main-banner__text">Make U Burger</h1>
  </div>
</template>
<script>
export default {
  name: "Banner",
};
</script>
<style scoped>
.main-banner {
  background-image: url("../assets/burger.jpg");
  background-position: center;
  background-size: cover;
  height: 500px;
  display: flex;
  align-items: center;
  justify-content: flex-start;
}
.main-banner__text {
  color: #fcba03;
  text-align: center;
  font-size: 60px;
  background: #222;
  padding: 40px;
  border-top-right-radius: 40px;
  border-bottom-right-radius: 40px;
}
</style>
