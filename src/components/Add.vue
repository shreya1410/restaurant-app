<template>
 <Header />
<h1>Add Restaurant</h1>
  <form class="add">
    <input  type="text" placeholder="Enter name" v-model="restaurant.name" name="name">
    <input  type="text" placeholder="Enter address" v-model="restaurant.address" name="address">
    <input  type="number" placeholder="Enter contact" v-model="restaurant.contact" name="contact">
    <button type="button" v-on:click="addRestaurant">Add new Restaurant</button>
  </form>
</template>

<script>
import axios from 'axios'
import Header from "@/components/Header";
export default {
name: "Add",
  data(){
  return{
    restaurant :{
      name :'',
      address :'',
      contact :''
    }
  }
  },
  components: {Header},
  methods:{
  async  addRestaurant(){
   //  console.log(this.restaurant)
    let result = await axios.post("http://localhost:3000/restaurants",{
      name : this.restaurant.name,
      address  : this.restaurant.address,
      contact : this.restaurant.contact
    });
    //console.log(result)
    if(result.status == 201)
    {
      this.$router.push({name:'Home'});
    }


    }
  }
}
</script>

<style scoped>

</style>
