<template>
    <div class="movie-page">
        <img :src="movie.Poster" :alt="movie.title">
        <h2> {{ movie.Title }} </h2>
        <p>{{ movie.Plot }}</p>
    </div>    
</template>

<script>
import { ref, onBeforeMount } from 'vue'
import { useRoute } from 'vue-router'
import env from '../env'

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();

        onBeforeMount(() => {
            fetch(`http://www.omdbapi.com/?apikey=${env.apiKey}&i=${route.params.id}&plot=full`)
                .then(response => response.json())
                .then(data => {
                    movie.value = data
                    console.log(data);
                });
        });

        return {
            movie
        }
    }
}
</script>

<style>
.movie-page img {
    width: 100%;
    height: 460px;
    object-fit: cover;
}
.movie-page h2 {
    color: #fff;
    margin-top: 12px;
    margin-left: 12px;
    font-size: 30px;
}
.movie-page p {
    color: #fff;
    line-height: 26px;
    padding-top: 10px;
    font-size: 19px;
    margin: 12px;
}
</style>