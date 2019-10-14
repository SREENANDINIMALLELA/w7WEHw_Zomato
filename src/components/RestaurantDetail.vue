<template lang="html">
<div>
  <h1>{{restaurantDetail.name}}</h1>
  <p>{{restaurantDetail.events_url}}</p>
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
