<template lang="html">
  <div class="flex-container">
    <label for="Restaurants">Restaurants  : </label>
    <select  @change="restaurantMethod($event)">
      <option value="" selected disabled hidden>Select Restaurant </option>
      <option v-for ="restaurant in restaurantsList.restaurants" :value='restaurant.name'>{{restaurant.name}}</option>
    </select>
    <div class="map" >
      <l-map :zoom="zoom" :center="center">
        <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
        <l-marker v-for = "marker in restaurantsList.markers":lat-lng="marker.position"
        v-on:l-add="realMarkerAdd">
        <l-popup :content="marker.tooltip"/>
      </l-marker>
    </l-map>
  </div>
  <RestaurantDetail v-bind:restaurantDetail="selectedRestaurant"/>
</div>
</template>






<script>
import RestaurantDetail from './RestaurantDetail'
import {LMap, LTileLayer, LMarker,LPopup } from 'vue2-leaflet'
export default {
  name: "Restaurants",
  data(){
    return{
      selectedRestaurant:{},
      zoom:13,
      center: [55.858174, -4.244168],
      url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
    }
  },
  props: ["restaurantsList"],
  components:{
    RestaurantDetail,LMap, LTileLayer, LMarker,LPopup
  },
  methods:{
    restaurantMethod: function(event){
      let selectedRes = event.target.value;
      this.selectedRestaurant = this.restaurantsList.restaurants.find(r => r.name == selectedRes);
    },
    realMarkerAdd: function(event){
      Vue.nextTick(() => {
        event.target.openPopup();
      })
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
.map {
  position: absolute;
  top: 350px;
  right:350px;
  width: 70vh;
  height: 50vh;
  border: 3px solid #73AD21;
}
/* .flex-container {
display: flex;
background-color: DodgerBlue;
} */
</style>
