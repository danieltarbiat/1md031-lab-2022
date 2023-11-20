<template>
  <section class="burgerSelect">
    <h2>
      Select your burger
    </h2>
    <p>Choose the burger that calls to you!</p>
      <BurgerContainerComponent
          @orderedBurgers="sendOrderToParent($event)"
      />
    <MapDivComponent
        @setLocation="sendLocationToParent($event)" />
  </section>

</template>

<script>
import BurgerContainerComponent from "@/components/BurgerContainerComponent.vue";
import MapDivComponent from "@/components/MapDivComponent.vue";
export default {
  name: "BurgerSectionComponent",
  components: {
    MapDivComponent,
    BurgerContainerComponent,
  },
  data:function () {
    return {
      orderedBurgers: {}
    }
  },
  methods: {
    sendOrderToParent: function (event) {
      this.orderedBurgers[event.name] = event.amount;
      this.$emit('orderedBurgers', event)
    },
    sendLocationToParent: function(event) {
      this.$emit('setLocation', event)
    }
  }

}
</script>

<style>
.burgerSelect {
  margin:10px;
  border: 5px dotted black;
  padding-left: 10px;
}

</style>