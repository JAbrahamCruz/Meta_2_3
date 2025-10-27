<template>
    <v-card class="pa-4">
        <v-img :src="movie.Poster" height="300"></v-img>
        <v-card-title>{{ movie.Title }}</v-card-title>
        <v-card-subtitle>{{ movie.Year }} - {{ movie.Genre }}</v-card-subtitle>
        <v-card-text>{{ movie.Plot }}</v-card-text>
        <v-btn color="primary" @click="$emit('close-details')">Cerrar</v-btn>
    </v-card>
</template>

<script setup>
const props = defineProps({
    movie: Object
})
const emit = defineEmits(['close-details'])
</script>