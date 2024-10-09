<template>
  <button @click="fetchData">Mostrar datos Api 1</button>

  <div v-if="data.length > 0">
    <h3>Countries API 1</h3>
    <ul>
      <li v-for="(country, index) in data" :key="index">
        {{ country.country }} - Población: {{ country.populationCounts[0].value }}
      </li>
    </ul>
  </div>
  
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const data = ref([]);

const fetchData = async () => {
  try {
    const response = await axios.get('https://countriesnow.space/api/v0.1/countries/population');
    data.value = response.data.data;
    console.log(response.data.data);
  } catch (error) {
    console.error('Error al obtener la información:', error);
  }
}

</script>
