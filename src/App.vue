<template>
  <div id="app">
    <table>
    <thead>
      <tr>
        <th> ID </th>
        <th> Name </th>
        <th> Username </th>
        <th> email </th>
        <th> Address </th>
        <th> Phone Number </th>
        <th> Website </th>
        <th> Company Name </th>
        <th> Company Product </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in searchResults" :key="item">
       <td>{{item.id}}</td> 
       <td>{{item.name}}</td>
       <td>{{item.username}}</td>  
       <td>{{item.email}}</td>  
       <td>{{item.address.street}}, {{item.address.suite}}, {{item.address.city}} {{item.address.zipcode}}</td>  
       <td>{{item.phone}}</td>  
       <td>{{item.website}}</td>  
       <td>{{item.company.name}}</td>  
       <td>{{item.company.bs}}</td>  
    </tr>
    </tbody>
    </table>

    <input type="text"
         placeholder="Search Name"
         v-model="searchName" />
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return{
      searchName:'',
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
  },

  computed:{
    searchResults(){
      if(this.searchName){
        return this.data.filter(info => {
        let nameField = info.name.toString().toLowerCase();
        let findName = this.searchName.toLowerCase();
        return nameField.includes(findName);
      })
      }else{
        return this.data;
      }
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
