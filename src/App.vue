<script setup>
  import PaginationComp from './components/PaginationComp.vue';
import SearchInput from './components/SearchInput.vue'
  import WeatherCards from './components/WeatherCards.vue';
  import { ref } from 'vue';

  const places = ref([])
  const addPlace = (data) => {
    places.value.push(data)
  }

  const deletePlace = (name) => {
    places.value = places.value.filter(p => p.location.name !== name)
  }
</script>

<template>
  <main>
    <!-- Date  -->
    <div class="text-center mb-6">
      {{ new Date().toLocaleDateString('en-us', {
        weekday: 'long',
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      }) }}
    </div>

    <!-- Search -->
     <div>
      <SearchInput @place-data="addPlace"/>
     </div>

    <!-- weather Cards -->
     <div class="grid grid-cols-2 gap-4 mr-4">
       <div v-for="(place, idx) in places" :key="idx">
          <WeatherCards :place="place" @delete-place="deletePlace"/>
       </div>

     </div>

    <!-- Pagination -->
     <PaginationComp :places="places"/>
  </main>
</template>

<style scoped>

</style>
