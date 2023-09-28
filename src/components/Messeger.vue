<template>
  <div class="messeger-container">
    <p>{{ msg }}</p>
  </div>
</template>
<script>
export default {
  name: "Messeger",
  props: {
    msg: String,
  },
};
</script>
<style scoped>
.messeger-container {
  color: #2c8500;
  background: #deffcc;
  border: 2px solid #c5ffb8;
  border-radius: 10px;
  padding: 10px;
  max-width: 400px;
  margin: 30px auto;
  text-align: center;
}
</style>
