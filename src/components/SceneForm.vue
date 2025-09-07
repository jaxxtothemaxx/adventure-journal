<script setup>
import { ref } from 'vue';

const emit = defineEmits(['save-scene']);

const newScene = ref({
  title: '',
  notes: '',
  status: 'Not Started',
});

function saveScene() {
  // Emit the new scene data to the parent component
  emit('save-scene', { ...newScene.value });
  // Reset the form
  newScene.value.title = '';
  newScene.value.notes = '';
}
</script>

<template>
  <form @submit.prevent="saveScene" class="bg-white p-6 rounded-lg shadow-md mb-6">
    <h3 class="text-2xl font-bold mb-4">Add New Scene</h3>
    <div class="mb-4">
      <input v-model="newScene.title" class="w-full p-2 border rounded text-gray-800" placeholder="Scene Title" required />
    </div>
    <div class="mb-4">
      <textarea v-model="newScene.notes" class="w-full p-2 border rounded text-gray-800" placeholder="Scene Notes"></textarea>
    </div>
    <button type="submit" class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded">Save Scene</button>
  </form>
</template>