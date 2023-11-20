<template>
    <button @click="orderBurger" class="orderButton">
      <img src="../../public/img/send.png" alt="" style="width: 25px; height: 25px">
      Order
    </button>
</template>
<script>
import io from 'socket.io-client'

const socket = io();
export default {
  name: "ButtonComponent",
  props: {
    fullName: String,
    email: String,
    payment: String,
    gender: String,
    orderedBurgers: Object,
    location: Object,
    orderNumber: Number,
  },
  methods: {
    atleastOneBurgerOrdered(arrayOfBurgerAmount) {
      return arrayOfBurgerAmount === 0;},
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top};
      this.location = {x: event.clientX - 10 - offset.x,
        y: event.clientY - 10 - offset.y}
    },
    increaseOrderNumber() {
      this.orderNumber++;
    },
    orderBurger: function () {
      if (Object.values(this.orderedBurgers).every(this.atleastOneBurgerOrdered)) {
        alert("Please order at least one burger");
        return;
      }
      if(this.fullName === "" ) {
        alert("Please fill in your full name");
        return;
      }
      if (this.email === "") {
        alert("Please fill in your email");
        return;
      }
      this.increaseOrderNumber();
      this.$emit('orderPlaced', this.orderNumber);
      socket.emit("addOrder", { orderId: this.orderNumber,
            details: { x: this.location.x,
              y: this.location.y },
            orderItems: this.orderedBurgers,
            customerInfo: { "Full Name": this.fullName,
              "Email": this.email,
              "Payment Method": this.payment,
              "Gender": this.gender }
          }
      );
    },
  }
}
</script>

<style>
.orderButton {
  margin: 20px 10px 10px;
}
.orderButton:hover {
  background-color: springgreen;
  cursor: pointer;
}
</style>