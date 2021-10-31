<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <ul id="userList">
      <li v-for="item in data" :key="item.name">
         {{item.name}}
      </li>
    </ul>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  data() {
    return{
      data:{}
    }
  },

  beforeMount() {
    this.getUsers();
  },

  methods: {
    async getUsers(){
      const userRequest = new Request(
        "https://jsonplaceholder.typicode.com/users", {
          method: "GET",
          mode:"cors",
          cache: "default"
        }
      );

      let testRequest = await fetch(userRequest);
      this.data = await testRequest.json();
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
