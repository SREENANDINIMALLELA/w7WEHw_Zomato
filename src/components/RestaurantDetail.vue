<template lang="html">
  <div>
    <h1>{{restaurantDetail.name}}</h1>
  </div>
</template>

<script>
export default {
  name: "RestaurantDetail",
  props: ["restaurantDetail"]
}
</script>

<style lang="css" scoped>
</style>
