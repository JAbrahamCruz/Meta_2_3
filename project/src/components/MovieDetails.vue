<!-- MovieDetails.vue -->
<template>
    <v-overlay v-model="internalVisible" :scrim="true" opacity="0.8" class="d-flex align-center justify-center">
        <v-card width="500" elevation="10" class="pa-4">
            <v-img :src="movie.Poster" height="300" cover class="mb-3"></v-img>
            <v-card-title class="text-h5">{{ movie.Title }}</v-card-title>
            <v-card-subtitle class="mb-2">{{ movie.Year }} • {{ movie.Genre }}</v-card-subtitle>
            <v-card-text>{{ movie.Plot }}</v-card-text>

            <v-card-actions class="d-flex justify-end">
                <v-btn color="primary" @click="closeDetails">Cerrar</v-btn>
            </v-card-actions>
        </v-card>
    </v-overlay>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
    visible: Boolean,
    movie: Object
})

const emit = defineEmits(['close-details'])

// Para vincular v-model del overlay
const internalVisible = ref(props.visible)

watch(() => props.visible, (val) => {
    internalVisible.value = val
})

const closeDetails = () => {
    internalVisible.value = false
    emit('close-details')
}
</script>
