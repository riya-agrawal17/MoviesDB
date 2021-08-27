<template>
  <div class="movie-detail">
    <h1>{{ movie.Title }}</h1>
    <p class="ye">{{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
    <p class="lines">{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from '@/env.js';
export default {
  setup() {
    const movie = ref({});
    const route = useRoute();
    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
        });
    });
    return {
      movie,
    };
  },
};
</script>

<style lang="scss">
.movie-detail {
  padding: 16px;
  h1 {
    color: #fff;
    font-size: 28px;
    font-weight: 600;
    margin-bottom: 16px;
    margin-left: 600px;
  }
  .ye {
    margin-left: 680px;
  }
  .featured-img {
    display: block;
    max-width: 220px;
    margin-top: 10px;
    margin-bottom: 20px;
    margin-left: 630px;
  }
  .lines {
    margin-left: 250px;
    margin-right: 250px;
  }
  p {
    color: #fff;
    font-size: 18px;
    line-height: 1.4;
  }
}
</style>
