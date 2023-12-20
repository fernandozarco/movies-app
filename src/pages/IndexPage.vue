<template>
  <q-page class="flex flex-center">
    <div class="q-my-">
      <label for="">Busca por titulo</label>
      <input type="text" v-model="query">
      <button @click="searchMovies">Buscar</button>
    </div>

    <div class="q-pa-md row items-start q-gutter-md" style="width: 100%;">
      <MovieCard v-for="movie in movies" :key="movie.imdbID" :movieData="movie" @click="showMovie(movie.imdbID)" />
      <!-- <q-card class="my-card" v-for="movie in movies" :key="movie.imdbID">
        <q-img :src="movie.Poster" @click="showMovie(movie.imdbID)">
          <div class="absolute-bottom text-subtitle2 text-center">
            {{ movie.Title }}
          </div>
        </q-img>
      </q-card> -->
    </div>

    <q-dialog v-model="card">
      <MoviePage :movieData="movie" />
      <!-- <q-card class="my-card">
        <q-img :src="movie.Poster" />

        <q-card-section>
          <div class="row no-wrap items-center">
            <div class="col text-h6 ellipsis">
              {{ movie.Title }}
            </div>
          </div>

          <q-rating v-model="stars" :max="5" size="32px" />
        </q-card-section>

        <q-card-section class="q-pt-none">
          <div class="text-subtitle1">
            {{ movie.Director }}
          </div>
          <div class="text-caption text-grey">
            {{ movie.Actors }}
          </div>
        </q-card-section>

        <q-separator />

        <q-card-actions align="right">
          <q-btn v-close-popup flat color="primary" label="Add favorites" />
        </q-card-actions>
      </q-card> -->
    </q-dialog>
  </q-page>
</template>

<style scoped>
.my-card {
  width: 100%;
  max-width: 250px;
}
</style>

<script>
import axios from 'axios'
import { ref } from 'vue'
import MoviePage from 'src/pages/MoviePage.vue'
import MovieCard from 'src/components/MovieCard.vue'

export default {
  name: 'IndexPage',
  components: {
    MoviePage,
    MovieCard
  },
  setup() {
    const movies = ref([])
    const query = ref('')
    const card = ref(false)
    const movie = ref({})

    async function searchMovies() {
      console.log('search mvies', query.value)
      const { data } = await axios.get(`https://www.omdbapi.com/?apikey=bad0d056&s=${query.value}`)
      console.log('data', data)
      movies.value = data.Search
      console.log('movies dta', movies.value)
    }

    async function showMovie(movieId) {
      console.log('showMovie(movie.imdbID)', movieId)
      const { data } = await axios.get(`https://www.omdbapi.com/?apikey=bad0d056&i=${movieId}`)
      console.log('movie', data)
      movie.value = data
      card.value = true
    }

    return {
      movies,
      movie,
      query,
      card,
      searchMovies,
      showMovie
    }
  }
}
</script>
