<template>
  <div>
    <h1 class="text-2xl font-bold mb-4">Add Form</h1>
  </div>
  <form class="space-y-4" @submit.prevent="addRecipe">
    <div>
      <input
        class="p-2 border rounded w-full"
        type="text"
        v-model="name"
        placeholder="Recipe name"
        required
      />
    </div>
    <div>
      <textarea
        class="p-2 border rounded w-full"
        v-model="description"
        placeholder="Recipe description"
        required
      ></textarea>
    </div>
    <button class="px-4 py-2 bg-orange-600 text-white rounded hover:bg-orange-700" type="submit">
      Add
    </button>
  </form>
</template>

<script setup lang="ts">
import { useRecipeStore } from '@/stores/recipe';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const name = ref('');
const description = ref('');

const router = useRouter();

const store = useRecipeStore();

const addRecipe = () => {
  const recipe = store.addRecipe({
    name: name.value,
    description: description.value,
  });

  router.push({
    name: 'recipe',
    params: {
      id: recipe.id,
    },
  });
};
</script>
