<template>
  <div class="burgerDiv">
    <h3>
      {{ burger.name }}
    </h3>
    Amount to order: {{ amountOrdered }}<br>
    <button @click="increaseBurgerAmount" class="increaseBurgerButton">+</button>
    <button @click="decreaseBurgerAmount" class="decreaseBurgerButton">-</button>
    <br>
    <img v-bind:src="burger.img" style="width: 400px; height: 300px;">
    <ul>
      <section class="allergies">
        <li>{{ burger.lactose }} </li>
        <li>{{ burger.gluten }}</li>
      </section>
    </ul>
  </div>
  </template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object,
    },
    data: function () {
      return {
        amountOrdered: 0,
      }
    },
    methods: {
      increaseBurgerAmount: function () {
        this.amountOrdered++;
        this.$emit('orderedBurgers', {name: this.burger.name,
          amount: this.amountOrdered})
      },
      decreaseBurgerAmount: function () {
        if (this.amountOrdered > 0) {
        this.amountOrdered--;
        this.$emit('orderedBurgers', {name: this.burger.name,
            amount: this.amountOrdered})
      }
        }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  .burgerDiv {
    padding: 2px;
    margin: 5px;
  }

  .increaseBurgerButton:hover {
    background-color: limegreen;
  }
  .decreaseBurgerButton:hover {
    background-color: crimson;
  }
  </style>
  