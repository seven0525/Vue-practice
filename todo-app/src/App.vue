<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <form v-on:submit.prevent>
      <input type="text" v-model="newItem"></input>
      <button v-on:click="addItem">add</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos">
        <input type="checkbox" v-model="todo.isDone"></input>
        <span v-bind:class="{done: todo.isDone}">{{ todo.item }}</span>
        <button v-on:click="deleteItem(index)">Delete</button>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Todo-List',
      newItem: "",
      todos: [],
    }
  },
  methods: {
    addItem: function(){
      if(this.newItem == "") return;
      var todo = {
        item: this.newItem,
        isDone: false
      };
      this.todos.push(todo);
      this.newItem = ""
    },
    deleteItem: function(index){
      this.todos.splice(index, 1)
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
  // display: inline-block;
  margin: 0 10px;
}
li > span.done {
  text-decoration: line-through;
}

a {
  color: #42b983;
}


</style>
