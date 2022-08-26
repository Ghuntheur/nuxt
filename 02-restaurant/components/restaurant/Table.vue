<template>
  <div class="table">
    <h1>TOP 50: THE RANKING</h1>
    <div class="table-container">
      <div class="table-col">
        <RestaurantRow
          v-for="restaurant in restaurantsOrganized.first"
          :key="restaurant.id"
        />
      </div>
      <div class="table-col">
        <RestaurantRow
          v-for="restaurant in restaurantsOrganized.second"
          :key="restaurant.id"
        />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import restaurants from '@/data.json'

const restaurantsOrganized = {
  first: restaurants.slice(0, 25),
  second: restaurants.slice(25, 50)
}
</script>

<style scoped>
.table {
  margin: 3rem 0;
}
.table h1 {
  margin-bottom: 2rem;
}
.table-container {
  display: flex;
  justify-content: space-between;
}
.table-col {
  width: 48%;
}
</style>
