<template lang="html">
  <div>
    <label for="Restaurants">Restaurants  : </label>
  <select>
    <option value="" selected disabled hidden>Select Restaurant </option>
    <option v-for ="restaurant in restaurants1" :value='restaurant.name'>{{restaurant.name}}</option>
  </select>
</div>
</template>

<script>
export default {
  name: "Restaurants",
  props: ["restaurants1"]
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
