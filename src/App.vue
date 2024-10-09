<template>
  <button @click="fetchData">Mostrar datos Api 1</button>

  <div v-if="data1.length > 0">
    <h3>Countries API 1</h3>
    <ul>
      <li v-for="(country, index) in data1" :key="index">
        {{ country.country }} - Población: {{ country.populationCounts[0].value }}
      </li>
    </ul>
  </div>

  <button @click="fetchData2">Mostrar datos Api 2</button>

  <div v-if="data2.length > 0">
    <h3>Anime API 2</h3>
    <ul>
      <li v-for="anime in data2" :key="anime.mal_id">
        <img :src="anime.image" :alt="anime.title" />
        <p>{{ anime.title }}</p>
      </li>
    </ul>
  </div>

  <button @click="fetchData3">Mostrar datos Api 3</button>

  <div v-if="data3.length > 0">
    <h3>Wish Cat API 3</h3>
    <ul>
      <li v-for="anime in data3" :key="anime.mal_id">
        <img :src="anime.image" :alt="anime.title" />
        <p>{{ anime.title }}</p>
      </li>
    </ul>
  </div>

  <button @click="fetchData4">Mostrar datos Api 4</button>

  <div v-if="data4.length > 0">
    <h3>Random Manga API 4</h3>
    <ul>
      <li v-for="manga in data4" :key="manga.mal_id">
        <img :src="manga.image" :alt="manga.title" />
        <p>{{ manga.title }}</p>
      </li>
    </ul>
  </div>
  
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';

const data1 = ref([]);

const data2 =ref([]);

const data3 =ref([]);

const data4 =ref([]);


const fetchData = async () => {
  try {
    const response = await axios.get('https://countriesnow.space/api/v0.1/countries/population');
    data1.value = response.data.data;
    console.log(response.data.data);
  } catch (error) {
    console.error('Error al obtener la información:', error);
  }
}

const fetchData2 = async () => {
  try {
    const response = await axios.get('https://api.jikan.moe/v4/recommendations/anime');
    data2.value = response.data.data.map(anime =>({
      mal_id: anime.entry[0].mal_id,
      title: anime.entry[0].title,
      image: anime.entry[0].images.jpg.image_url
    }));
    console.log(response.data.data);
  } catch (error) {
    console.error('Error al obtener la información:', error);
  }
}
const fetchData3 = async () => {
  try {
    const response = await axios.get('https://api.jikan.moe/v4/random/anime');
    const anime = response.data.data;
    data3.value = [{
        mal_id: anime.mal_id,
        title: anime.title,
        image: anime.images.jpg.image_url
    }];
    console.log(anime);
  } catch (error) {
    console.error('Error al obtener la información:', error);
  }
}
const fetchData4 = async () => {
  try {
    const response = await axios.get('https://api.jikan.moe/v4/random/manga');
    const manga = response.data.data;
    
    data4.value = [{
        mal_id: manga.mal_id,
        title: manga.title,
        image: manga.images.jpg.image_url
    }];
    
    console.log(manga); 
  } catch (error) {
    console.error('Error al obtener la información:', error);
  }
}
</script>
