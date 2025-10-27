<template>
    <v-form>
        <v-container class="d-flex flex-row ga-2 pa-0">
            <v-text-field v-model="formData.query" label="Search Movie" placeholder="E.g Inception" />
            <v-select v-model="formData.type" :items="types" item-title="text" item-value="value" label="Type"
                placeholder="E.g Movie, series, episode" />
            <v-number-input v-model="formData.year" label="Year" placeholder="E.g 1997" :min="1950" :max="new Date().getFullYear()"/>
        </v-container>
        <v-container class="d-flex flex-row justify-space-evenly">
            <v-btn @click="onSearch" width="30%" color="primary">Search</v-btn>
            <v-btn @click="onClear" width="30%" variant="outlined" color="primary">Reset</v-btn>
        </v-container>
    </v-form>
</template>

<script setup>
import { reactive } from 'vue'

const formData = reactive({
    query: '',
    type: '',
    year: null
})

const types = [
    { text: 'Movie', value: 'movie' },
    { text: 'Series', value: 'series' },
    { text: 'Episode', value: 'episode' }
]

const emit = defineEmits(['search-movies', 'clear-results'])

const onSearch = () => {
    emit('search-movies', { query: formData.query, type: formData.type, year: formData.year })
}

const onClear = () => {
    formData.query = ''
    formData.type = ''
    formData.year = null
    emit('clear-results')
}
</script>

<style scoped>
* {
    border: 1px solid white;
}
</style>