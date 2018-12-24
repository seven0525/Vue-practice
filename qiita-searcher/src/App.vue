<template>
  <div id="app">
    <img src="./assets/logo.png">
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      items: null,
      keyword: "",
      message: ""
    }
  },
  watch: {

  },
  created: function(){
    this.keyword = "JavaScript"
    this.getAnswer()

  },
  methods: {
    getAnswer: function(){
      if(this.keyword == "") {
        this.items = null
        return
      }

      this.message = "Loading..."
      var vm = this
      var params = { page:1, per_page:20, query:this.keyword}
      axios.get("https://qiita.com/api/v2/items", { params})
        .then(function(response){
          console.log(response)
          vm.items = response.data
        })
        .catch(function(error){
          vm.message = "Error" + error
        })
        .finally(function(response){
          vm.message = ""
        })

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
</style>
