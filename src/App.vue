<template>
  <div id="app">
    <div>
      <b-navbar
        toggleable="lg"
        type="dark"
        variant="warning"
        class="mb-4"
      >
        <b-navbar-brand href="#">ZenShop</b-navbar-brand>
      </b-navbar>
    </div>
    <Cart />
  </div>
</template>


<script>
import Cart from "./components/Cart";

export default {
  name: "app",
  components: {
    Cart,
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #081018;
  background-color: rgb(219, 207, 253);
  /* margin-top: 60px; */
}

/* Head{
  color:blueviolet;

} */
</style>
