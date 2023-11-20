<template>
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
</template>

<script>
export default {
  name: "CustomerInfoSection",
  data: function () {
    return {
      fullName: "",
      email: "",
      payment: "Swish",
      gender: "Do not wish to provide",
    }
  },
  watch: {
    fullName: function (newName) {
      if (newName === "") {
        alert("Please fill in your full name.")
      }
      else {
        this.$emit("changedFullName", newName)
        console.log(newName)
      }
    },
    email: function (newEmail) {
      if (newEmail === "") {
        alert("Please fill in your email.")
      }
      else {
        this.$emit("changedEmail", newEmail)
      }
    },
    payment: function (newPaymentOption) {
      this.$emit("changedPaymentOption", newPaymentOption)
    },
    gender: function (newGenderOption) {
      this.$emit("changedGenderOption", newGenderOption)
  }
}
}
</script>

<style>
.customerInfo {
  margin: 10px;
  background-color: black;
  color: white;
  border: 5px dotted white;
  padding-left: 10px;
}
</style>