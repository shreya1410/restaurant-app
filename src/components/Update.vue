<template>
  <Header />
<h1>Update</h1>
  <form class="update">
    <input  type="text" placeholder="Enter name" v-model="restaurant.name" name="name">
    <input  type="text" placeholder="Enter address" v-model="restaurant.address" name="address">
    <input  type="text" placeholder="Enter contact" v-model="restaurant.contact" name="contact">
    <button type="button" v-on:click="updateRestaurant">Update new Restaurant</button>
  </form>
</template>

<script>
import axios from 'axios'
import Header from "@/components/Header";
export default {
  name: "Update",

  components: {Header},
  data() {
    return {
      restaurant: {
        name: '',
        address: '',
        contact: ''
      }
    }
  },
  methods:{
  async  updateRestaurant(){
      let result = await axios.put("http://localhost:3000/restaurants/"+ this.$route.params.id,
          {
        name : this.restaurant.name,
        address  : this.restaurant.address,
        contact : this.restaurant.contact
      });
      //console.log(result)
      if(result.status == 200)
      {
        this.$router.push({name:'Home'});
      }
    }
  },
  async mounted() {
    const result = await axios.get("http://localhost:3000/restaurants/"+
    this.$route.params.id);
   // console.log(result)
    this.restaurant = result.data
  }
}
</script>

<style scoped>

</style>
