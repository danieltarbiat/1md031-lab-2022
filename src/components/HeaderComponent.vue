<template>
  <header class="header">
    <h1 id="headline">
      Welcome to BurgerTown!
    </h1>
  </header>
</template>
<script>
export default {
  name: "HeaderComponent"
}
</script>

<style>
.header {
  display: grid;
  background-image: url("https://www.shutterstock.com/shutterstock/photos/2212297943/display_1500/stock-vector-burger-fast-food-restaurant-advertisement-promo-poster-vector-template-2212297943.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  opacity: 80%;
  margin: 10px;
  height: 650px;
  padding: 2px;
  grid-auto-columns: auto;
  grid-template-rows: 1fr 1fr;
  place-items: center;
  text-align: center;
}

#headline {
  color: white;
  text-shadow: 2px 2px black;

}
</style>
