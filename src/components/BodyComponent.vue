<template>
  <body>
  <HeaderComponent/>
  <MainComponent
      :burgers="burgers"
      @changedFullName="changeFullName($event)"
      @changedEmail="changeEmail($event)"
      @changedPayment="changePayment($event)"
      @changedGender="changeGender($event)"
      @orderedBurgers="updateOrder($event)"
      @setLocation="location = $event.location"
  />
  <ButtonComponent
      :full-name="fullName"
      :email="email"
      :payment="payment"
      :gender="gender"
      :ordered-burgers="orderedBurgers"
      :location="location"
      :order-number="orderNumber"
      @orderPlaced="orderNumber = $event"
  />
  <FooterComponent/>
  </body>
</template>

<script>
import HeaderComponent from "@/components/HeaderComponent.vue";
import MainComponent from "@/components/MainComponent.vue";
import ButtonComponent from "@/components/ButtonComponent.vue";
import FooterComponent from "@/components/FooterComponent.vue";


// Menu item constructor (not used so uncommented)
//function MenuItem (name, kCal, gluten, lactose, img) {
//  this.name = name;
//  this.kCal = kCal;
//  this.gluten = gluten;
//  this.lactose = lactose;
//  this.img = img;
//}
export default {
  name: "BodyComponent",
  components: {
    HeaderComponent,
    MainComponent,
    ButtonComponent,
    FooterComponent
  },
  data: function () {
    return {
      burgers:"",
      fullName: "",
      email: "",
      payment: "Swish",
      gender: "Do not wish to provide",
      orderedBurgers: {},
      location: {},
      orderNumber: 1
    }
  },
  methods: {
    updateOrder: function (event) {
      this.orderedBurgers = event;
    },
    changeFullName: function (event) {
      this.fullName = event;
    },
    changeEmail: function (event) {
      this.email = event;
    },
    changePayment: function (event) {
      this.payment = event;
    },
    changeGender: function (event){
      this.gender = event;
    }
  }
}

</script>

<style>
body {
  font-family: sans-serif;
}
</style>