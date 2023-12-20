<template>
  <q-card class="my-card">
    <q-img :src="movieData.Poster" />

    <q-card-section>
      <div class="row no-wrap items-center">
        <div class="col text-h6 ellipsis">
          {{ movieData.Title }}
        </div>
      </div>

      <q-rating v-model="stars" :max="5" size="32px" />
    </q-card-section>

    <q-card-section class="q-pt-none">
      <div class="text-subtitle1">
        {{ movieData.Director }}
      </div>
      <div class="text-caption text-grey">
        {{ movieData.Actors }}
      </div>
    </q-card-section>

    <q-separator />

    <q-card-actions align="right">
      <q-btn v-close-popup flat color="primary" label="Add favorites" />
    </q-card-actions>
  </q-card>
</template>

<script>
import { onMounted } from 'vue'
export default {
  name: 'MoviePage',
  props: {
    movieData: Object
  },
  setup(props) {

    onMounted(() => {
      console.log('shego al movie ', props.movieData)
    })
    return {}
  }
}
</script>

<style></style>