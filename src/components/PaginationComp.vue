<script setup>
import { ref } from 'vue';

const props = defineProps({
  places: Array,
  placesPerPage: {
    type: Number
  }
})

console.log(props.places.length);

const currentPage = ref(1)

</script>

<template>
  <div class="pagination">
    <ul class="pageList">
      <li class="pageLink" @click="changePage(currentPage - 1)" :disabled="currentPage === 1">
        Back
      </li>
      <li class="pageLink">1</li>
      <li class="pageLink">2</li>
      <li class="pageLink" @click="changePage(currentPage + 1)" :disabled="currentPage === places.length">
        Next</li>
    </ul>
  </div>

</template>

<style lang="css">
  .pagination{
    position: fixed;
    bottom: 25px;
    left: 45%;
    justify-content: center;
  }

  .pageList{
    display: flex;
  }

  .pageLink{
    border: 1px solid #feb002;
    border-radius: 5px;
    padding: 3px 10px;
    margin-right: 5px;
    text-align: center;
    background-color: #ffec03;
    cursor: pointer;
  }
</style>



