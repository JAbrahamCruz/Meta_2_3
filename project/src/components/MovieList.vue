<template>
    <v-row>
        <v-col v-for="movie in movies" :key="movie.imdbID" cols="12" xs="12" sm="6" md="4" lg="2">
            <v-card @click="emit('select-movie', movie.imdbID)">
                <v-img :src="movie.Poster" height="250"></v-img>
                <v-card-title>{{ movie.Title }}</v-card-title>
                <v-card-subtitle>{{ movie.Year + ' - ' + movie.Type }}</v-card-subtitle>
                <v-btn @click="emit('select-movie', movie.imdbID)" variant="plain" color="primary">See
                    details</v-btn>
            </v-card>
        </v-col>
    </v-row>
</template>

<script setup>
const props = defineProps({
    movies: Array
})
const emit = defineEmits(['select-movie'])
</script>
