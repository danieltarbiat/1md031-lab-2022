<template>
  <div class="burgerContainer">
    <Burger v-for="burger in burgers"
            v-bind:burger="burger"
            v-bind:key="burger.name"
            @orderedBurgers="addToOrder($event)"/>
  </div>

</template>


<script>
import Burger from "@/components/OneBurger.vue";
import menu from "@/assets/menu.json";

const menuArray = JSON.parse(JSON.stringify(menu));
export default {
  name: "BurgerContainerComponent",
   components: {
     Burger
   },
  data:function () {
    return {
      burgers: menuArray,
      orderedBurgers: {}
    }
  },
  methods: {
    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
      this.$emit('orderedBurgers', this.orderedBurgers)
    }
  }
}
</script>


<style>
.burgerContainer {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  overflow: scroll;
}
</style>