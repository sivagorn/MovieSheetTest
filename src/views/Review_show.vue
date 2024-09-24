<template>
    <div class="container">
      <div class="card"
        v-for="review in state.reviews" 
        :key="review.index">
        <div class="card-content">
          <p class="movie-title">{{ review.movie_name }}</p>
          <br>
          <p class="movie-rating">{{ review.rating }}</p>
          <br>
          <p class="movie-comment">{{ review.comment }}</p>
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
    reviews: [] 
  });
  
  onMounted(() => {
    const url = 'https://script.google.com/macros/s/AKfycbzABRWHUuJyCth8H-Ri9-aSwEHa3SX8-Kvs8Oop6miNuZpV3awOTd0H5yZuwopu3Bca/exec';
    axios.get(url)
      .then((response) => {
        state.reviews = response.data; 
        console.log(state.reviews);
      })
      .catch((error) => {
        console.error('Error fetching reviews:', error);
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
    border: 5px solid #ffffff;
    box-sizing: border-box;
    background-color: #ffffff;
  }
  
  .card-content {
    padding: 1rem;
    text-align: center;
  }
  
  .movie-title {
    font-size: 20px;
    margin: 0;
    color: rgb(0, 0, 0);
  }
  </style>
  