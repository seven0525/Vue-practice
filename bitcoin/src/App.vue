<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <h2 v-if="hasError">
      Error
    </h2>
    <div v-if="loading">
      Loading....
    </div>
    <ul v-cloak>
      <li v-for="(rate, currency) in bpi">
        {{  currency }} : {{ rate.rate_float | currencyDecimal}}
      </li>
    
    </ul>
  </div>
</template>


<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Bitcoin Price',
      bpi: null,
      hasError: false,
      loading: true
    }
  },
  mounted: function() {
    axios.get("https://api.coindesk.com/v1/bpi/currentprice.json")
    .then(function(response){
      // console.log(response.data.bpi.USD.rate_float)
      this.bpi = response.data.bpi
    }.bind(this))
    .catch(function(error){
      console.log(error)
      this.hasError = true
    }.bind(this))
    .finally(function(){
      this.loading = false
    }.bind(this))
  },
  filters: {
    currencyDecimal(value){
      return value.toFixed(2)
    }
  }
}
</script>





<style lang="scss">
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

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

[v-cloak]{
  display: none;
}
</style>
