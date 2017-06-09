<template>
  <div id="app">
    <h1>Calculate whether you'll lose more money renting an apartment or buying a home</h1>
    <div class="form">
      <div class="form-home-costs">
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
          <span class="form-item-label">Mortgage Length (in years)</span>
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
      </div>
      <div class="form-rent-costs">
        <div>
          <span class="form-item-label">Monthly Rent</span>
          <input class="form-item" type="number" v-model="rentMonthCost" placeholder="rent per month" >
        </div>
        <div>
          <span class="form-item-label">Renters Insurance</span>
          <input class="form-item" type="number" v-model="rentInsurance" placeholder="renters insurance (annual)" >
        </div>
      </div>
    </div>
    <div class="totals">
      <div class="totals-home">
        <div>
          <span class="output-item">Total Due at Closing</span>
          <span class="output-item">${{ dueAtClose }}</span>
        </div>
        <div>
          <span class="output-item">Monthly Mortgage Payment</span>
          <span class="output-item">${{ monthlyMortgagePayment }}</span>
        </div>
        <div>
          <span class="output-item">Monthly Mortgage Insurance</span>
          <span class="output-item">${{ monthlyMortgageInsurance }}</span>
        </div>
        <div>
          <span class="output-item">Total Monthly Payment</span>
          <span class="output-item">${{ monthlyTotalPayment }}</span>
        </div>
      </div>
      <div class="totals-rent">
        <div>
          <span class="output-item">Annual Rent Cost</span>
          <span class="output-item">${{ rentAnnual }}</span>
        </div>
        <div>
          <span class="output-item">Total to Rent</span>
          <span class="output-item">${{ totalRentAnnual }}</span>
        </div>
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
      rentInsurance:  500,
      rentMonthCost: 1900,
      yearlyPropertyTaxes: 5200
    }
  },
  computed: {
    dueAtClose: function() {
      return this.downPayment + this.closingCosts;
    },
    loanAmount: function() {
      return this.homeCost - this.downPayment;
    },
    monthlyMortgageInsurance: function() {
      return parseFloat(this.loanAmount * this.mortgageInsuranceRate / 12).toFixed(2);
    },
    monthlyMortgagePayment: function() {
      return parseFloat(( (this.homeCost - this.downPayment) * (this.interestRate / 12) ) / (1 - Math.pow((1 + (this.interestRate/12)), (-1 * this.mortgageLength * 12)))).toFixed(2);
    },
    monthlyTotalPayment: function() {
      return parseFloat(parseFloat(this.monthlyMortgagePayment) + this.annualInsurance / 12 + this.yearlyPropertyTaxes / 12 + this.monthlyMortgageInsurance).toFixed(2);
    },
    rentAnnual: function() {
      return parseFloat(this.rentMonthCost * 12).toFixed(2);
    },
    totalRentAnnual: function() {
      return parseFloat( parseFloat(this.rentAnnual) + this.rentInsurance ).toFixed(2);
    },
  },
  toDollar: function(numberSting) {
    let [dollars, cents] = numberString.split('.');

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

.form {
  display: flex;
}

.form-home-costs {
  flex: 1 1 50%;
}

.form-rent-costs {
  flex: 1 1 50%;
}

.totals {
  display: flex;
  margin-top: 5rem;
}

.totals-home {
  flex: 1 1 50%;
}

.totals-rent {
  flex: 1 1 50%;
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
