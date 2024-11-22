<script setup>
import { ref } from 'vue';
import BorderLine from './BorderLine.vue'
import WeatherForecastDay from './WeatherForecastDay.vue'
import WeatherInfo from './WeatherInfo.vue';

defineProps({
  place: Object
})

const emit = defineEmits(['delete-place'])

const removePlace = (placeName) => {
  emit('delete-place', placeName)
  showDetails.value = false
}

const showDetails = ref(false)

</script>

<template>
  <div :class="place.current.is_day === 0 ? 'bg-night' : 'bg-day' " class="text-white p-10 rounded-lg shadow-lg gap-6 mb-6 relative overflow-hidden">
    <!-- Location & time -->
    <div class="mb-2 flex justify-between items-center">
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-location-dot"></i>
        <h1 class="text-3xl">{{ place.location.name }}, {{ place.location.country }}</h1>
      </div>
      <div class="flex items-center justify-center gap-2">
        <i class="fa-solid fa-clock"></i>
        <h1 class="text-3xl">
          {{ new Date(place.location.localtime).getHours() }}:
          {{ new Date(place.location.localtime).getMinutes() }}
        </h1>
      </div>
    </div>

    <!-- current weather -->
    <div class="text-center flex-1">
      <img :src="place.current.condition.icon" alt="icon" width="200" class="mx-auto -mb-10" />
      <h1 class="text-9xl mb-2">{{ Math.round(place.current.temp_c) }}&deg;</h1>
      <p class="text-2xl">{{ place.current.condition.text }}</p>
    </div>

    <BorderLine />

    <!-- forecast -->
    <div v-for="(day, idx) in place.forecast.forecastday" :key="idx">
      <WeatherForecastDay :day="day"/>
    </div>

    <!-- info -->
     <Transition name="fade">
      <div v-show="showDetails">
        <WeatherInfo :place="place"
        @close-info="showDetails=false"
        @remove-place="removePlace(place.location.name)"/>
      </div>
  </Transition>

    <!-- forecast btn -->
    <div class="flex justify-end items-center gap-1 mt-10">
      <button @click="showDetails = true">More <i class="fa-solid fa-arrow-right text-sm -mb-px"></i></button>
    </div>
  </div>
</template>

<style scoped>
  .bg-day{
    background-color: rgb(29, 181, 236);
  }

  .bg-night{
    background-color: rgba(0, 0, 0, 0.934);
  }

  .fade-enter-active,
  .fade-leave-active {
  transition: opacity 0.3s ease;
  }

  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
  }
</style>
