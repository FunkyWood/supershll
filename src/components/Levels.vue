<template>
  <div class="flex items-center justify-center min-h-screen p-4 overflow-auto">
    <!-- Levels -->
    <div class="w-3/4 max-w-screen-md mx-auto">
      <div v-for="level in levels" :key="level.id" class="card bordered max-w-xl mx-auto py-4 shadow-md">
        <!-- Level media (image or video) -->
        <div class="relative" style="padding-bottom: 56.25%">
          <img v-if="level.media && level.media.type === 'image'" :src="level.media.url" :alt="`Image for ${level.title}`" class="absolute w-full h-full object-cover">
          <iframe v-else-if="level.media && level.media.type === 'video'" :src="level.media.url" title="YouTube video player" class="absolute w-full h-full"></iframe>
        </div>
        <!-- Level details -->
        <div class="card-body">
          <h2 class="text-2xl">{{ level.title }}</h2>
          <p>{{ level.description }}</p>
          <div class="justify-end card-actions">
            <div class="text-gray-500">By: {{ level.user }}</div>
            <div class="text-gray-500">Level ID: {{ level.levelId }}</div>
            <div class="text-gray-500">WR: {{ level.wr ? level.wr : 'N/A' }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

// Reactive variables
const levels = ref([]);
const showModal = ref(false);

// Fetch levels on component mounted
onMounted(async () => {
  const res = await fetch('https://raw.githubusercontent.com/FunkyWood/urban-guide/main/levels.json');
  levels.value = await res.json();
});

// Functions to open and close the modal
const openModal = () => {
  showModal.value = true;
};
const closeModal = () => {
  showModal.value = false;
};
</script>

<style scoped>
img {
  max-width: 100%;
}
</style>

<style>
body {
  margin: 0;
  padding: 0;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
