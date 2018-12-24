<template>
  <div id="app">
    <p>
      <input type="text" v-model="keyword"></input>
    </p>
    <p>
     {{ message}}
    </p>
    <ul>
      <li v-for="item in items">
        <a v-bind:href="item.url" target="_blank">{{ item.title }}</a> likes:{{ item.likes_count }}
      </li>
    </ul>


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
    keyword: function(newKeyword, oldKeyword){
      this.message = "Waiting for you to stop typing ..."
      this.debouncedGetAnswer()
    }

  },
  created: function(){
    // this.keyword = "JavaScript"
    // this.getAnswer()
    this.debouncedGetAnswer = _.debounce(this.getAnswer, 1000)

  },
  methods: {
    getAnswer: function(){
      if(this.keyword == "") {
        this.items = null
        this.message = ""
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
// #app {
//   font-family: 'Avenir', Helvetica, Arial, sans-serif;
//   -webkit-font-smoothing: antialiased;
//   -moz-osx-font-smoothing: grayscale;
//   text-align: center;
//   color: #2c3e50;
//   margin-top: 60px;
// }

// h1, h2 {
//   font-weight: normal;
// }

// ul {
//   list-style-type: none;
//   padding: 0;
// }

// li {
//   // display: inline-block;
//   margin: 0 10px;
// }

a {
  color: #42b983;
}
</style>
