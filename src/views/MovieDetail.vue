<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';
import { useRoute } from 'vue-router';

const route = useRoute();
const state = reactive({
  movies: [],
  movie: null
});

onMounted(() => {
  const url = 'https://script.googleusercontent.com/macros/echo?user_content_key=6Zaipk-Qwe6VZ7ZqU8w2ZU90rICEwPtRs_EN3rbBjYdiOdHts-WyF0FLutmgMvKXLfk05TWB6dwWOc15I_EyID6t_lap3DAgm5_BxDlH2jW0nuo2oDemN9CCS2h10ox_1xSncGQajx_ryfhECjZEnL8u_AcB_1UHpYPCdf8vF9NY5MH5fDAIIq05qmQpVHYvIVZediGCqp9VPBpAUZwcVLrWvMx9lReKudZEoNYGr_Nl257qV3UnLQ&lib=MlS1jc-5j_78AMWoObAbgVkPwlNntp4vT';
  
  axios.get(url)
    .then((response) => {
      state.movies = response.data;
      const movieId = parseInt(route.params.index); 
      state.movie = state.movies.find(movie => movie.movie_id === movieId);
    })
    .catch((error) => {
      console.error('Error fetching movies:', error);
    });
});

const getYoutubeId = (url) => {
  const regExp = /(?:youtube\.com\/(?:[^\/]+\/[^\/]+\/|(?:v|e(?:mbed)?)\/|.*[?&]v=)|youtu\.be\/)([^"&?\/ ]{11})/;
  const match = url.match(regExp);
  return match ? match[1] : null;
};
</script>

<template>
  <AppLayout>
    <div v-if="state.movie" class="movie-card-container">
      <div class="movie-card">
        <img :src="state.movie.poster" alt="Poster">
        <div class="card-content">
          <h2>{{ state.movie.title }}</h2>
          <p>
            <b>ตัวอย่างภาพยนต์</b><br>
            <iframe 
              v-if="state.movie.trailer" 
              width="640" 
              height="360" 
              :src="`https://www.youtube.com/embed/${getYoutubeId(state.movie.trailer)}`" 
              title="YouTube video player" 
              frameborder="0" 
              allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
              allowfullscreen>
            </iframe><br><br>
            <b>เรื่องย่อ</b><br>
            {{ state.movie.synopsis }}
            <br><br>
            <b>ประเภท</b><br>
            {{ state.movie.genres }}
            <br><br>
            <b>ความยาว</b><br>
            {{ state.movie.duration }}
            <br><br>
            <b>ผู้กำกับ</b><br>
            {{ state.movie.director }}
            <br><br>
            <b>นักแสดง</b><br>
            {{ state.movie.cast }}
            <br><br>
            <b>สถานะ</b><br>
            -{{ state.movie.status }}-
            <br>
          </p>
        </div>
      </div>
    </div>
  </AppLayout>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Anton&family=Itim&family=Kodchasan:ital,wght@1,600&family=Mali&family=Mooli&family=Nunito:wght@500&family=Roboto+Slab&family=Sriracha&display=swap');

h1 {
  font-family: "Anton", sans-serif;
  font-weight: 500;
  font-style: normal;
}

.movie-card-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.movie-card {
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 20px;
  padding: 20px;
  width: 80%;
  max-width: 800px;
  margin-top: 700px;
}

.movie-card img {
  max-width: 38%;
  border-radius: 20px;
}

.card-content {
  font-family: "Anton", sans-serif;
  margin-left: 20px;
  margin-top: 30px;
}

.card-content h2 {
  font-size: 30px;
  margin-bottom: 10px;
}

.card-content p {
  font-size: 20px;
}
</style>
