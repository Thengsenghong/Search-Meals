<template>
  <div class="flex flex-col p-8">
    <input
      type="text"
      class="rounded border-2 border-gray-300 w-full"
      placeholder="Search for Meals"
    />
    <div class="flex justify-center gap-2 mt-2">
      <router-link :to="{name: 'byLetter', params: { letter }}" v-for="letter of letters" :key="letter">
        {{ letter }}
      </router-link>
    </div>
    <pre>{{ ingredients }}</pre>
  </div>
</template>
<script setup>
import { onMounted, ref } from 'vue';
import axiosClient from '../axiosClient'


const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXIZ'.split('') 
const ingredients = ref([])

onMounted(async() => {
  const response = await axiosClient.get('/list.php?i=list')
  ingredients.value = response.data
})
</script>
