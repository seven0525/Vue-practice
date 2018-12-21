<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>{{ msg }}</h1>
    <a v-if="toggle" v-bind:href="url">Vue.js公式</a>
    <textarea v-model="msg"></textarea>
    <button v-on:click="clickHandler">Click</button>
    <ul v-for="language in languages">{{ language }}</ul>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      url: "https://github.com/seven0525",
      toggle: true,
      languages: ["Python","Ruby","React"]
    }
  },
  methods: {
    clickHandler: function(){
      this.msg="clicked!";
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
