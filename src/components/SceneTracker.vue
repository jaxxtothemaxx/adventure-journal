<script setup>
import { ref } from 'vue';
import SceneForm from './SceneForm.vue';

// A reactive array to hold multiple scenes.
const scenes = ref([
  {
    id: 1,
    title: 'The Adventure Begins',
    notes: 'The heroes meet in a tavern, unaware of the dangers that lie ahead.',
    status: 'In Progress',
  },
]);

const showForm = ref(false);

function handleSaveScene(newScene) {
  scenes.value.push({ id: Date.now(), ...newScene });
  showForm.value = false; // Hide form after saving
}
</script>

<template>
  <div class="p-8">
    <div class="flex justify-between items-center mb-4">
      <h1 class="text-3xl font-bold">Adventure Journal</h1>
      <button @click="showForm = !showForm" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded">
        {{ showForm ? 'Cancel' : 'Add Scene' }}
      </button>
    </div>

    <SceneForm v-if="showForm" @save-scene="handleSaveScene" />

    <div
      v-for="scene in scenes" :key="scene.id"
      class="relative bg-cover bg-center p-6 rounded-lg shadow-lg mb-4"
      style="background-image: url('/assets/journal-template.png')"
    >
      <h2 class="text-2xl font-bold text-gray-800">{{ scene.title }}</h2>
      <p class="mt-2 text-gray-600">{{ scene.notes }}</p>
      <span class="absolute top-4 right-4 bg-blue-500 text-white px-2 py-1 text-sm rounded">{{ scene.status }}</span>
    </div>
  </div>
</template>