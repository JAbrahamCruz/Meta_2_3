<template>
  <v-container min-height="100vh" height="auto" class="d-flex flex-column">
    <v-row class="flex-grow-0" style="height: auto">
      <v-col cols="12">
        <h1 class="text-h1 text-center">🎬 Movie Hunter</h1>
      </v-col>
    </v-row>

    <v-row class="flex-grow-0" style="height: auto">
      <v-col cols="12">
        <!-- Aqui se buscaran las peliculas -->
        <MovieSearch @search-movies="handleSearch" @clear-results="handleClear" />
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <!-- Aqui se mostraran las peliculas -->
        <!-- <LoadingSpinner :loading="loading" /> -->

        <MovieList v-if="movies.length > 0" :movies="movies" @select-movie="handleMovieSelect" />

        <MovieDetails v-if="selectedMovie" :movie="selectedMovie" @close-details="handleCloseDetails" />

        <v-alert v-if="error" type="error" class="mt-4">
          {{ error }}
        </v-alert>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'
import MovieSearch from '@/components/MovieSearch.vue'
import MovieList from '@/components/MovieList.vue'
import MovieDetails from '@/components/MovieDetails.vue'
import LoadingSpinner from '@/components/LoadingSpinner.vue'
import { searchMovies, getMovieDetails } from '@/services/api'

const movies = ref([])
const selectedMovie = ref(null)
const loading = ref(false)
const error = ref('')

const handleSearch = async (searchParams) => {
  loading.value = true
  error.value = ''

  try {
    console.log(searchParams)
    const response = await searchMovies(searchParams)
    console.log('Respuesta de API: ', response)
    if (response.Search) {
      movies.value = response.Search
    } else {
      movies.value = []
      error.value = 'No movies found'
    }
  } catch (err) {
    error.value = 'Error al buscar películas'
    console.error(err)
  } finally {
    loading.value = false
  }
}

const handleMovieSelect = async (imdbID) => {
  loading.value = true
  try {
    selectedMovie.value = await getMovieDetails(imdbID)
  } catch (err) {
    error.value = 'Error al cargar detalles de la película'
    console.error(err)
  } finally {
    loading.value = false
  }
}

const handleCloseDetails = () => {
  selectedMovie.value = null
}

const handleClear = () => {
  movies.value = []
  selectedMovie.value = null
  error.value = ''
}
</script>

<style scoped>
* {
  border: 1px solid;
}
</style>