<template lang="html">
  <div>
    <label for="Restaurants">Restaurants  : </label>
    <select  @change="restaurantMethod($event)">
      <option value="" selected disabled hidden>Select Restaurant </option>
      <option v-for ="restaurant in restaurants1" :value='restaurant.name'>{{restaurant.name}}</option>
    </select>
    <RestaurantDetail v-bind:restaurantDetail="selectedRestaurant"/>
  </div>
</template>

<script>
import RestaurantDetail from './RestaurantDetail'
export default {
  name: "Restaurants",
  data(){
    return{
      selectedRestaurant:{}
    }
  },
  props: ["restaurants1"],
  components:{
    RestaurantDetail
  },
  methods:{
    restaurantMethod: function(event){
      let selectedRes = event.target.value;
      this.selectedRestaurant = this.restaurants1.find(r => r.name == selectedRes);
      console.log(this.selectedRestaurant);
    }
  }
}
  </script>



  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
    h3 {
      margin: 40px 0 0;
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
