<template>
  <Header />
<h1>Welcome  {{name}}</h1>
  <table border="1px">
    <th>Id</th>
    <th> Restaurant Name</th>
    <th>Restaurant Address</th>
    <th>Restaurant Contact</th>
    <th>Actions</th>
    <tr v-for="item in restaurants" v-bind:key="item.id">
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.address}}</td>
      <td>{{item.contact}}</td>
      <td>
        <router-link :to="'/update/'+item.id">Update</router-link>
        <button v-on:click="deleteRestaurant(item.id)">delete</button>
      </td>
    </tr>
  </table>
</template>

<script>
import axios  from "axios";
import Header from "@/components/Header";
export default {
  name: "Home",
  data(){
    return {
      name:'',
      restaurants :[],
    }
  },
  components: {Header},
  methods:{
  async  deleteRestaurant(id){
     // console.log(id)
      let result =await  axios.delete(" http://localhost:3000/restaurants/"+id);
      if(result.status==200)
      {
        this.loadData()
      }

    },
    async loadData(){
      let user =localStorage.getItem("user-info");
      this.name = JSON.parse(user).name
      if(!user)
      {
        this.$router.push({name: 'Signup'})
      }
      let result =await  axios.get(" http://localhost:3000/restaurants");
      //  console.log(result)
      this.restaurants = result.data
    }
  },
  mounted() {
    this.loadData()

  }
}
</script>

<style scoped>
td
{
  width: 160px;
  height: 40px;
}
table{
  width: 1000px;
  margin-left: 100px;
}
th{
  color: brown;
  background-color: aquamarine
}
</style>
