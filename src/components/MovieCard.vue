<template>
  <q-card class="movie-card">
    <q-img :src="movieData.Poster">
      <div class="absolute-bottom text-subtitle2 text-center">
        {{ movieData.Title }}
      </div>
    </q-img>
  </q-card>
</template>

<script>
import { onMounted } from 'vue'
export default {
  name: 'MovieCard',
  props: {
    movieData: Object
  },
  setup(props) {

    onMounted(() => {
      console.log('Movie card', props.movieData)
    })
    return {}
  }
}
</script>

<style scoped>
.movie-card {
  width: 100%;
  max-width: 250px;
}
</style>