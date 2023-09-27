<template>
  <div id="nav">
    <router-link to="/" id="logo_url">
      <img :src="logo" :alt="alt" id="logo" />
    </router-link>
    <router-link to="/">HOME</router-link>
    <router-link to="/orders">ORDERS</router-link>
  </div>
</template>
<script>
export default {
  name: "NavBar",
  props: ["logo", "alt"],
};
</script>
<style scoped>
* {
  font-family: Helvetica, sans-serif;
}
#nav {
  background-color: #222;
  border-bottom: 4px;
  padding: 15px 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
#nav #logo_url {
  margin: auto;
  margin-left: 0;
}
#logo {
  width: 40px;
  height: 40px;
}
#nav a {
  color: #fcba03;
  text-decoration: none;
  margin: 12px;
  transition: 0.5s;
}
#nav a:hover {
  color: white;
  cursor: pointer;
}
</style>
