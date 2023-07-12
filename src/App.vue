<script setup lang="ts">
import {ref} from "vue";

interface Restaurant {
  name?: string
  status?: RestaurantStatus
  dishes?: Dish[]
}

enum RestaurantStatus {
  WanttoTry = 'Want to Try',
  DoNotRecommend = 'Do Not Recommend',
  Delicious = 'Delicious'
}

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

function addRestaurant() {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    status: newRestaurant.value.status,
    dishes: []
  })
}
</script>

<template>
  <main>
  <pre>
  {{ newRestaurant }}
  </pre>
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text"/>
      </div>
      <div class="select">
        <label for="restaurant-name">Restaurant Status</label>
        <select v-model="newRestaurant.status" id="status">
          <option v-for="status in Object.values(RestaurantStatus)" :value="status" :key="`option-${status}`">
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
<ul>
  <li v-for="resaurant in restaurantList" :key="resaurant.name">
    {{resaurant.name}} - {{resaurant.status}}
  </li>
</ul>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}


nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
