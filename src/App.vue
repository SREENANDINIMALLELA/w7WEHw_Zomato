<template lang="html">


  <div >
    <label for="cities">City  : </label>
    <select @change="cityMethod($event)" >
      <option value="" selected disabled hidden>Select city</option>
      <option v-for ="city in cities" :value='city.value'>{{city.name}}</option>
    </select>
    <br/>
    <Restaurants v-bind:restaurants1="restaurantInfos"/>
  </div>


</template>

<script>

import Restaurants from './components/Restaurants'


export default {
  name: "app",
  data(){

    return{
      cities:[
        {name: 'Edinburgh',
        value:76},
        {name:'Glasgow',
        value: 77
      }
    ],
    restaurantInfos:{
      restaurants : [],
      markers: []
    }
  }
},
components: {
  Restaurants
},
methods: {
  cityMethod:function(event){
    let cityId = event.target.value
    fetch('https://developers.zomato.com/api/v2.1/search?entity_id='+cityId+'&entity_type=city',{
      headers:{
        'user-key':'068ba0cac95a295a4ba5cd3909aa17c5'
      }
    })
    .then(response => response.json())
    .then(data => {


      let markers = []
      let restaurants = data.restaurants.map(res => res.restaurant)
      //let locations =  restaurants.map(res => res.location);
      for (var i = 0; i < restaurants.length; i++) {
        let marker = {position: '', tooltip: ''}
        let ps = {lat:'',lng:''}
        ps.lat = restaurants[i].location.latitude
        ps.lng = restaurants[i].location.longitude
        marker.position = ps
        marker.tooltip = restaurants[i].name

        markers.push(marker)
      }

      this.restaurantInfos.restaurants = restaurants
      this.restaurantInfos.markers = markers
    })

  }
}
}
</script>

<style lang="css" scoped>

</style>
