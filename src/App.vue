<template lang="html">

  <div>
    <label for="cities">City  : </label>
    <select @change="cityMethod($event)" >
      <option value="" selected disabled hidden>Select city</option>
      <option v-for ="city in cities" :value='city.value'>{{city.name}}</option>
    </select>
    <br/>
    <select>
      <option value="" selected disabled hidden>Select Restaurant </option>
      <option v-for ="restaurant in restaurants" :value='restaurant.name'>{{restaurant.name}}</option>
    </select>
  </div>

</template>

<script>
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
      restaurants:[]
    }
  },
  methods: {
    cityMethod:function(event){
    let cityId = event.target.value
    console.log(cityId);

    fetch('https://developers.zomato.com/api/v2.1/search?entity_id='+cityId+'&entity_type=city',{
      headers:{
        'user-key':'068ba0cac95a295a4ba5cd3909aa17c5'
      }
    })
    .then(response => response.json())
    .then(data => {
      console.log(data);
      this.restaurants = data.restaurants.map(res => res.restaurant)
    })

    }
  }
}
</script>

<style lang="css" scoped>
</style>
