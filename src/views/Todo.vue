<template>
    <div>
      <header>
        <h1>Total à payer: 12000 FCFA</h1>
        <div class="payment-options">
          <PaymentOption
            v-for="option in paymentOptions"
            :key="option.type"
            :icon="option.icon"
            :label="option.label"
            :isActive="selectedOption === option.type"
            @toggle="togglePaymentOption(option.type)"
          />
        </div>
      </header>
  
      <form v-if="selectedOption !== 'credit-card'">
        <div class="form-group">
          <label for="name">Nom et Prénom :</label>
          <input type="text" id="name" v-model="name" />
        </div>
  
        <div class="form-group">
          <label for="phone">Numéro de téléphone :</label>
          <input type="tel" id="phone" v-model="phone" />
        </div>
  
        <div class="payment-btn">
          <button @click.prevent="handlePayment" :style="{ backgroundColor: 'red' }">
            Payer 12000 FCFA
          </button>
        </div>
      </form>
  
      <h1 v-else>Pas encore disponible</h1>
    </div>
  </template>
  
  <script>
  import PaymentOption from "./PaymentOption.vue";
  
  export default {
    components: {
      PaymentOption,
    },
    data() {
      return {
        name: "",
        phone: "",
        selectedOption: "", 
        paymentOptions: [
          {
            type: "mobile",
            label: "Mobile",
            icon: "mobile-icon.png", 
          },
          {
            type: "credit-card",
            label: "Carte de crédit",
            icon: "credit-card-icon.png",
          },
        ],
      };
    },
    methods: {
      togglePaymentOption(option) {
        this.selectedOption = option;
      },
      handlePayment() {
        
        console.log("Payment successful!");
      },
    },
  };
  </script>
  
  <style>
 
  header {
    text-align: center;
  }
  
  .payment-options {
    display: flex;
    justify-content: center;
  }
  
  .form-group {
    margin-bottom: 20px;
  }
  
  .payment-btn {
    text-align: center;
  }
  </style>
  
  
  <template>
    <div class="payment-option" @click="toggleActive">
      <img :src="icon" :alt="label" :class="{ active: isActive }" />
      <span>{{ label }}</span>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      icon: String,
      label: String,
      isActive: Boolean,
    },
    methods: {
      toggleActive() {
        this.$emit("toggle");
      },
    },
  };
  </script>
  
  <style>
  
  .payment-option {
    display: flex;
    flex-direction: column;
    align-items: center;
    cursor: pointer;
  }
  
  .payment-option img {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    border: 2px solid #ccc;
    padding: 5px;
  }
  
  .payment-option span {
    margin-top: 5px;
  }
  
  .payment-option img.active {
    border-color: red;
  }
  </style>
  
  
  <template>
    <div id="app">
      <PaymentForm />
    </div>
  </template>
  
  <script>
  import PaymentForm from "./components/PaymentForm.vue";
  
  export default {
    name: "App",
    components: {
      PaymentForm,
    },
  };
  </script>
  
  