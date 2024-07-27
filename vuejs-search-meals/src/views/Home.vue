<template>
    <div class="flex flex-col p-8">
        <input type="text" class="rounded border-2 border-gray-200 w-full" placeholder="Search for Meals...">

        <div class=" flex gap-2 justify-center mt-2">
            <router-link :to="{ name: 'byLetter', params: { letter } }" v-for="letter of letters" :key="letter">
                {{ letter }}
            </router-link>
        </div>
        <pre>{{ ingredients }}</pre>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import store from '../store'
import axiosClint from '../axiosClint.js'

// const meals = computed(() => store.state.meals)
const letters = 'ABCDEFGHIJKLMNOPQRSTUVXYZ'.split('')
const ingredients = ref([])
onMounted(async () => {
    const response = await axiosClint.get('/list.php?i=list')
    console.log(response.data);
    ingredients.value = response.data
})
</script>
