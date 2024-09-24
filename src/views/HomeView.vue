<template>
  <div class="container">
    <div 
      v-for="movie in state.movies" 
      :key="movie.movie_id" 
      class="card" 
      @click="goToDetail(movie.movie_id)"
  >
      <img class="poster" :src="movie.poster" alt="Poster">
      <div class="card-content">
        <p class="movie-title">{{ movie.title }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, reactive } from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';

const router = useRouter();

const state = reactive({
  movies: [] 
});

const goToDetail = (movie_id) => {
  router.push({ name: 'MovieDetail', params: { index: movie_id } }); 
}

onMounted(() => {
  const url = 'https://script.googleusercontent.com/macros/echo?user_content_key=6Zaipk-Qwe6VZ7ZqU8w2ZU90rICEwPtRs_EN3rbBjYdiOdHts-WyF0FLutmgMvKXLfk05TWB6dwWOc15I_EyID6t_lap3DAgm5_BxDlH2jW0nuo2oDemN9CCS2h10ox_1xSncGQajx_ryfhECjZEnL8u_AcB_1UHpYPCdf8vF9NY5MH5fDAIIq05qmQpVHYvIVZediGCqp9VPBpAUZwcVLrWvMx9lReKudZEoNYGr_Nl257qV3UnLQ&lib=MlS1jc-5j_78AMWoObAbgVkPwlNntp4vT';
  axios.get(url)
    .then((response) => {
      state.movies = response.data; 
      console.log(state.movies);
    });
});
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Anton&family=Itim&family=Kodchasan:ital,wght@1,600&family=Mali&family=Mooli&family=Nunito:wght@500&family=Roboto+Slab&family=Sriracha&display=swap');

.container {
  margin-top: 50px;
  display: flex;
  flex-wrap: wrap;
  gap: 3rem;
  padding-left: 70px;
}

.card {
  display: flex;
  flex-direction: column;
  width: 260px;
  border: 5px solid #ff0400;
  box-sizing: border-box;
  background-color: #b7a3ca;
}

.poster {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-content {
  padding: 1rem;
  text-align: center;
}

.movie-title {
  font-size: 20px;
  margin: 0;
  color: gold;
}
</style>
