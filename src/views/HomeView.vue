<template>
  <body>
  <header class="header">
    <h1 id="headline">
      Welcome to BurgerTown!
    </h1>
  </header>
  <main>
    <section class="burgerSelect">
      <h2>
        Select your burger
      </h2>
      <p>Choose the burger that calls to you!</p>
      <div>
        <div class="burgerContainer">
          <Burger v-for="burger in burgers"
                  v-bind:burger="burger"
                  v-bind:key="burger.name"
                  v-on:orderedBurgers="addToOrder($event)"/>
        </div>
        <div class="mapDiv">
          <div id="map" @click="setLocation">
            <div id="dots">
            <div v-bind:style="{ left: location.x + 'px',
                                top: location.y + 'px'}"
                 v-bind:key="'dots'">
              T </div>
          </div>
          </div>
        </div>

      </div>
    </section>
    <section class="customerInfo">
      <h2>
        Customer Information
      </h2>
      <p>
        Provide your details below.
      </p>
      <h2>Delivery information:</h2>
      <form id="customerInfo">
        <p>
          <label for="fullName">Full Name:</label><br>
          <input type="text" id="fullName" v-model="fullName" required="required" placeholder="First- and last name">
        </p>
        <p>
          <label for="email">E-Mail:</label><br>
          <input type="text" id="email" v-model="email" required="required" placeholder="E-mail adress">
        </p>
        <p>
          <label for="payment">Payment method:</label><br>
          <select id="payment" v-model="payment">
            <option value="Card">Card</option>
            <option value="Swish">Swish</option>
            <option value="Paypal">Paypal</option>
            <option value="Payment at delivery">Payment at delivery</option>
          </select>
        </p>
        <p>
          <label for="gender">Gender:</label><br>
          <input type="radio" id="male" v-model="gender" value="Male" required="required">
          <label for="male">Male</label><br>
          <input type="radio" id="female" v-model="gender" value="Female" required="required">
          <label for="female">Female</label><br>
          <input type="radio" id="nonB" v-model="gender" value="Non-Binary" required="required">
          <label for="nonB">Non-Binary</label><br>
          <input type="radio" id="doNotWish" v-model="gender" value="Do not wish to provide" required="required">
          <label for="doNotWish">Do not wish to provide</label><br>
        </p>

      </form>
    </section>

  </main>
  <button @click="orderBurger" class="orderButton">
    <img src="img/send.png" alt="" style="width: 25px; height: 25px">
    Order
  </button>
  <footer>
    <hr>
    All copyrights reserved
  </footer>
  </body>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import menu from '../assets/menu.json'
import io from 'socket.io-client'

const socket = io();


// Menu item constructor (not used so uncommented)
//function MenuItem (name, kCal, gluten, lactose, img) {
//  this.name = name;
//  this.kCal = kCal;
//  this.gluten = gluten;
//  this.lactose = lactose;
//  this.img = img;
//}

// Create burgers from menu JSON
const menuArray = JSON.parse(JSON.stringify(menu));
function atleastOneBurgerOrdered(arrayOfBurgerAmount) {
  return arrayOfBurgerAmount === 0;
}
export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menuArray,
      fullName: "",
      email: "",
      payment: "Swish",
      gender: "Do not wish to provide",
      orderedBurgers: {},
      location: {
        x: 0,
        y: 0
      },
      orderNumber: 1
    }
  },
  methods: {
    setLocation: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      this.location = {x: event.clientX - 10 - offset.x,
                       y: event.clientY - 10 - offset.y}

    },
    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
    },
    orderBurger: function () {
      if (Object.values(this.orderedBurgers).every(atleastOneBurgerOrdered)) {
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
      this.orderNumber++;
      console.log(
          this.fullName, "\n",
          this.email, "\n",
          this.payment,"\n",
          this.gender,"\n",
          this.orderedBurgers);
    },
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      this.location = {x: event.clientX - 10 - offset.x,
                       y: event.clientY - 10 - offset.y}
    },
  }
}
</script>

<style>
body {
  font-family: sans-serif;
}

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

.burgerSelect {
  margin:10px;
  border: 5px dotted black;
  padding-left: 10px;
}
.customerInfo {
  margin: 10px;
  background-color: black;
  color: white;
  border: 5px dotted white;
  padding-left: 10px;
}
.burgerContainer {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  overflow: scroll;
}

.orderButton {
  margin: 20px 10px 10px;
}
.orderButton:hover {
  background-color: springgreen;
}
.mapDiv {
  overflow: scroll;
}
#dots {
  position: relative;
  margin: 0;
  padding: 0;
  background-repeat: no-repeat;
  width:1920px;
  height: 1078px;
  cursor: crosshair;
}

#dots div {
  position: absolute;
  background: black;
  color: white;
  border-radius: 10px;
  width:20px;
  height:20px;
  text-align: center;
}
  #map {
    background: url("../../public/img/polacks.jpg");
    height: 1078px;
    width: 1920px;
  }
</style>