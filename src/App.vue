<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>

  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <a class="navbar-brand" href="#">Navbar</a>
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav">
        <li class="nav-item active">
          <RouterLink class="nav-link" to="/">ปุ่ม 1 <span class="sr-only">(current)</span></RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/reviews">ปุ่ม 2</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/review_show">ปุ่ม 3</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink class="nav-link" to="/reports">ปุ่ม 4</RouterLink>
        </li>
      </ul>
    </div>
  </nav>

  <!-- แสดงเนื้อหาตามการนำทาง -->
  <RouterView />
</template>

<style>
  body {
    background-color: #000000;
  }
</style>
