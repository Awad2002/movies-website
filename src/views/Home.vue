<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/asd123">
        <img src="https://image.cnbcfm.com/api/v1/image/106980045-1637766874360-Encanto_Cropped_1.jpg?v=1637767028&w=929&h=523" class="featured-image">
        <div class="details">
          <h3> Encanto (2021) </h3>
        <p>
          A young Colombian girl has to face the frustration of being the only member of her family without magical powers.
        </p>
        </div>
      </router-link>
    </div>
    <form class="search-box" @submit.prevent="SearchMovies">
      <input type="text" v-model="search" placeholder="What are you looking for?">
      <input type="submit" value="Search">
    </form>

    <div class="movies-list">
      <h3> Movies </h3>
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID">
          <div class="movie-img">
            <img :src="movie.Poster" :alt="movie.Title">
            <div class="type"> {{ movie.Type }} </div>
          </div>
          <div class="movie-content">
            <p> {{ movie.Year }} </p>
            <h4> {{ movie.Title }} </h4>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import env from '../env';

export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {
            movies.value = data.Search;
            search.value = "";
          })
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<style>
a {
  text-decoration: none !important;
}
.home .feature-card {
  position: relative;
}
.home .feature-card .featured-image {
  display: block;
  width: 100%;
  height: 300px;
  object-fit: cover;
  position: relative;
  z-index: 0;
}
.home .feature-card .details {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  padding: 16px;
  z-index: 1;
}
.home .feature-card .details h3 {
  color: #fff;
  margin-bottom: 16px;
}
.home .feature-card .details p {
  color: #fff;
}
.home .search-box {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 16px;
}
.home .search-box input {
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  width: 100%;
  color: #fff;
  background-color: #496583;
  font-size: 18px;
  padding: 10px 16px;
  border-radius: 8px;
  margin-bottom: 15px;
  transition: 0.4s;
}
.home .search-box input::placeholder {
    color: #f3f3f3;
}
.home .search-box input:focus {
  box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
}
.home .search-box input[type="submit"] {
  width: 100%;
  background-color: #42b883;
  padding: 11px;
  border-radius: 8px;
  color: #fff;
  font-size: 18px;
  text-transform: uppercase;
  transition: 0.4s;
}
.home .search-box input[type="submit"]:active {
  background-color: #3b8070;
}
.movies-list {
  padding: 16px;
  padding-top: 0 !important;
}
.movies-list h3 {
  color: #fff;
  margin-bottom: 12px;
}
.movies-list .movie {
  background-color: #4965838f;
  margin-bottom: 18px;
  border-radius: 8px;
  overflow: hidden;
  position: relative;
}
.movies-list .movie img {
  width: 100%;
  height: 246px;
  object-fit: cover;
}
.movies-list .movie .type {
  position: absolute;
  top: 14px;
  left: 14px;
  background-color: #204b41;
  font-size: 17px;
  padding: 8px 17px;
  border-radius: 8px;
  color: #fff;
}
.movies-list .movie .movie-content {
  padding: 14px;
}
.movies-list .movie .movie-content p {
  padding: 0;
  margin: 0;
  font-size: 16px;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.5);
  margin-bottom: 8px !important;
}
.movies-list .movie h4 {
  font-size: 22px;
  color: #fff;
  padding: 0 !important;
  margin: 0 !important;
}
</style>
