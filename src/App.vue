<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Calculate whether you'll lose more money renting an apartment or buying a home</h1>
    <div class="form">
      <div>
        <span class="form-item-label">Home Cost</span>
        <input class="form-item" type="number" v-model="homeCost" placeholder="home cost" >
      </div>
      <div>
        <span class="form-item-label">Down Payment</span>
        <input class="form-item" type="number" v-model="downPayment" placeholder="down payment" >
      </div>
      <div>
        <span class="form-item-label">Closing Costs</span>
        <input class="form-item" type="number" v-model="closingCosts" placeholder="closing costs" >
      </div>
      <div>
        <span class="form-item-label">Mortgage Length</span>
        <input class="form-item" type="number" v-model="mortgageLength" placeholder="mortgage length (in years)" >
      </div>
      <div>
        <span class="form-item-label">Loan Interest Rate</span>
        <input class="form-item" type="number" v-model="interestRate" placeholder="loan interest rate" >
      </div>
      <div>
        <span class="form-item-label">Annual Property Taxes</span>
        <input class="form-item" type="number" v-model="yearlyPropertyTaxes" placeholder="yearly property taxes" >
      </div>
      <div>
        <span class="form-item-label">Annual Insurance</span>
        <input class="form-item" type="number" v-model="annualInsurance" placeholder="annual insurance" >
      </div>
      <div>
        <span class="form-item-label">Mortgage Insurance Rate</span>
        <input class="form-item" type="number" v-model="mortgageInsuranceRate" placeholder="mortgageInsuranceRate" >
      </div>
      <div>
        <span class="output-item">Monthly Mortgage Payment</span>
        <span class="output-item">{{ monthlyMortgagePayment }}</span>
      </div>
      <div>
        <span class="output-item">Monthly Mortgage Insurance</span>
        <span class="output-item">{{ monthlyMortgageInsurance }}</span>
      </div>
      <div>
        <span class="output-item">Total Monthly Payment</span>
        <span class="output-item">{{ monthlyTotalPayment }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      annualInsurance: 1200,
      closingCosts: 8000,
      downPayment: 50000,
      homeCost: 430000,
      interestRate: .04,
      mortgageInsuranceRate: .003,
      mortgageLength: 30,
      msg: 'Welcome to Your Vue.js App that is cool',
      yearlyPropertyTaxes: 5200
    }
  },
  computed: {
    loanAmount: function() {
      return this.homeCost - this.downPayment;
    },
    monthlyMortgageInsurance: function() {
      return this.loanAmount * this.mortgageInsuranceRate / 12;
    },
    monthlyMortgagePayment: function() {
      return ( (this.homeCost - this.downPayment) * (this.interestRate / 12) ) / (1 - Math.pow((1 + (this.interestRate/12)), (-1 * this.mortgageLength * 12)));
    },
    monthlyTotalPayment: function() {
      return this.monthlyMortgagePayment + this.annualInsurance / 12 + this.yearlyPropertyTaxes / 12 + this.monthlyMortgageInsurance;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

input {
  display: block;
  margin: 0 auto;
  text-align: right;
}

a {
  color: #42b983;
}
</style>
