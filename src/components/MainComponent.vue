<template>
  <main>
    <BurgerSectionComponent
      @orderedBurgers="sendOrderToParent($event)"
      @setLocation="sendLocationToParent($event)"
    />
    <CustomerInfoSection
      @changedFullName="sendCustomerNameToParent($event)"
      @changedEmail="sendCustomerEmailToParent($event)"
      @changedPaymentOption="sendCustomerPaymentToParent($event)"
      @changedGenderOption="sendCustomerGenderToParent($event)"
  />
  </main>
</template>
<script>
import BurgerSectionComponent from "@/components/BurgerSectionComponent.vue";
import CustomerInfoSection from "@/components/CustomerInfoSection.vue";
export default {
  name: "MainComponent",
  components: {
    CustomerInfoSection,
    BurgerSectionComponent,
  },
  methods: {
    sendOrderToParent: function(event) {
      this.$emit('orderedBurgers', event)
    },
    sendLocationToParent: function(event) {
      this.$emit('setLocation', event)
    },
    sendCustomerNameToParent: function(event) {
      this.$emit('changedFullName', event)
    },
    sendCustomerEmailToParent: function(event) {
      this.$emit('changedEmail', event)
    },
    sendCustomerPaymentToParent: function(event) {
      this.$emit('changedPaymentOption', event)
    },
    sendCustomerGenderToParent: function(event) {
      this.$emit('changedGenderOption', event)
    }
  }
}
</script>

<style>

</style>